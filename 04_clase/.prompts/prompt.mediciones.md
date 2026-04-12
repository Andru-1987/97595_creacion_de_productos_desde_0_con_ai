
*Requisitos previos:*

- Tu backend ya tiene las tablas, RLS y Edge Function `validate-booking` (Sprints 1–6).
- El frontend está en Next.js 14 con Zustand, shadcn/ui y cliente de Supabase.
- Cuentas gratuitas en los servicios que elijas: **PostHog** o **Better Stack** (analytics), **Loops** o **Resend** (mensajería).

---

### Prompt 1 – Instrumentación de eventos (mínimo 5)

**Objetivo:** Capturar eventos clave del usuario para medir conversiones y KPIs.

```prompt

@file:src/lib/supabaseClient.ts 
@file:src/app/t/[tenantSlug]/dashboard/page.tsx 
@file:src/app/t/[tenantSlug]/reservas/page.tsx 
@file:src/app/t/[tenantSlug]/facturacion/page.tsx 
@file:src/app/t/[tenantSlug]/portal/page.tsx

Instala PostHog (o Better Stack) en el proyecto Next.js.

Crea un servicio `src/lib/analytics.ts` que exporte funciones para registrar eventos:
- `trackEvent(eventName: string, properties?: object)`

Instrumenta los siguientes eventos en sus respectivos componentes/páginas:
1. `login_success` – cuando el usuario inicia sesión (desde el store de Zustand).
2. `dashboard_view` – al cargar la página del dashboard.
3. `reservation_created` – después de crear una reserva exitosamente (usa la Edge Function validate-booking).
4. `reservation_cancelled` – cuando el usuario cancela una reserva.
5. `invoice_marked_paid` – cuando admin/owner marca una factura como pagada.

Cada evento debe incluir propiedades relevantes: `tenant_slug`, `user_role`, `space_type` (si aplica), `timestamp`.

Asegura que no se disparen eventos duplicados (idempotencia del lado del cliente) y que los errores de red no rompan la UI.
```

---

### Prompt 2 – Integración de mensajería transaccional (Loops / Resend)

**Objetivo:** Enviar correos automáticos (bienvenida, confirmación de reserva) usando un servicio SaaS externo.

```prompt
@file:supabase/functions/send-email/index.ts 
@file:src/app/api/webhooks/supabase/route.ts

Investiga la documentación de **Loops** o **Resend** y crea una cuenta gratuita.

1. Genera dos plantillas de correo en el servicio elegido:
   - **Bienvenida** (para nuevos miembros registrados)
   - **Confirmación de reserva** (incluye detalles: espacio, fecha, hora)

2. Implementa una **Edge Function de Supabase** (`send-email`) que reciba `{ to, templateId, data }` y llame a la API de Loops/Resend.

3. Configura un **webhook de base de datos** en Supabase:
   - Evento: `INSERT` en la tabla `reservations`
   - Destino: la Edge Function `send-email`
   - Envía `{ to: user.email, templateId: "reservation_confirmation", data: { space_name, starts_at, ends_at } }`

4. Para el correo de bienvenida, dispara desde un trigger de base de datos cuando se inserta un nuevo perfil (`profiles`).

5. Agrega **idempotencia** en la Edge Function: guarda un registro de envíos en una tabla `email_logs` (con `reservation_id` o `profile_id`) para evitar correos duplicados ante reintentos del webhook.

6. Prueba el flujo completo: crea una reserva desde el frontend y verifica que llegue el correo de confirmación.
```

---

### Prompt 3 – Diagrama de integración asíncrona

**Objetivo:** Visualizar el pipeline de un touchpoint (ej. creación de reserva).

```prompt
Genera un diagrama en formato **Mermaid** (para incluirlo en el README o documentación) que muestre el flujo completo de un evento de reserva:

1. Usuario hace clic en “Reservar” → frontend llama a Edge Function `validate-booking`
2. Edge Function inserta en Supabase (tabla `reservations`)
3. Webhook de base de datos detecta el INSERT y llama a la Edge Function `send-email`
4. `send-email` → API de Loops/Resend → correo al usuario
5. Paralelamente, desde el frontend se dispara el evento `reservation_created` hacia PostHog/Better Stack

El diagrama debe incluir:
- Componentes: Next.js (cliente), Supabase (DB + Edge Functions), servicio de email, servicio de analytics.
- Tipo de comunicación (asíncrona para email, síncrona para validación de reserva).
- Indicación de idempotencia en el webhook.

Escribe el código Mermaid y una breve explicación del flujo.
```

---

### Prompt 4 – Nota de privacidad y consentimiento

**Objetivo:** Cumplir con requisitos legales básicos (GDPR / CCPA).

```prompt
@file:src/app/t/[tenantSlug]/portal/page.tsx 
@file:src/components/auth/LoginForm.tsx

Agrega en el formulario de login y en la página del portal del miembro un enlace a una nueva página `/privacy`.

Crea `src/app/privacy/page.tsx` con una **Nota de privacidad** que incluya:

- Qué datos personales se recopilan (email, nombre, reservas, pagos).
- Finalidad (gestión del espacio de coworking, envío de correos transaccionales).
- Servicios externos utilizados (Supabase, PostHog/Better Stack, Loops/Resend) y sus respectivas políticas de privacidad.
- Derechos del usuario (acceso, rectificación, cancelación).
- Uso de cookies o localStorage (solo para sesión).
- Consentimiento explícito: un checkbox en el login que diga “Acepto el tratamiento de mis datos según la [nota de privacidad]”. Guarda esta preferencia en el perfil del usuario (columna `consent_given_at`).

Implementa que si el usuario no acepta, no pueda iniciar sesión (muestra un toast de error).
```

---

### Prompt 5 – Checklist final y validación

**Objetivo:** Verificar que todos los puntos de la clase están cubiertos.

```prompt
Genera un script de verificación automática o una lista de comprobación manual para validar:

- [ ] Existen al menos 5 eventos instrumentados (revisa `src/lib/analytics.ts` y su uso en componentes).
- [ ] Cada evento envía datos correctos a PostHog/Better Stack (puedes simular con modo desarrollo).
- [ ] El diagrama de integración (Mermaid) está presente en `docs/integration.md`.
- [ ] Las dos plantillas de correo (bienvenida, confirmación) están creadas en Loops/Resend.
- [ ] El webhook de Supabase envía correos al insertar una reserva.
- [ ] La Edge Function `send-email` implementa idempotencia.
- [ ] La nota de privacidad está publicada en `/privacy` y se solicita consentimiento en login.

Además, escribe un pequeño resumen de cómo este conjunto de herramientas (analytics + mensajería + backend asíncrono) transforma SpaceDesk en un **producto sostenible** orientado a KPIs.
```


---

### Tener en cuenta que es lo que se logra con esto

Un producto funcional que:

- Mide el comportamiento de los usuarios mediante eventos analíticos.
- Notifica por email las acciones críticas de forma asíncrona y confiable.
- Documenta la arquitectura y cumple con privacidad.
- Está listo para iterar basado en KPIs reales.