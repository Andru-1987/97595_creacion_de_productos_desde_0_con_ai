### CONTEXTO

- **CONTEXTO DEL PROYECTO: SaaS COWORKING MULTITENANT**
- **Objetivo:** Aplicación profesional de gestión de coworking.
- **Arquitectura:** Multitenant real (aislamiento por `tenant_id` y - subdominios dinámicos).
- **Tech Stack:** Vue.js, Supabase (con RLS), PWA, Tailwind CSS, Framer Motion.
- **Vibe:** Minimalismo de Squarespace + Eficiencia técnica de [Linear.app.](https://linear.app/) & [ICOMAT](https://www.icomat.co.uk/)
- **Reglas Críticas:** 1. Imports relativos (`../`). 2. Datos en `mockData.ts`. 3. PWA instalable. 4. Toasts para feedback.
- **Entidades:** Tenants, Profiles, Spaces, Reservations, Memberships, Payments, Announcements.

---

### PASO 1: Diseño UI/UX (Para STITCH)
*Este prompt se enfoca en la "piel" y la experiencia, asegurando que el diseño contemple la lógica multitenant.*

> **PROMPT 1: DESIGN SYSTEM & LAYOUTS**
> [PEGAR BLOQUE DE CONTEXTO AQUÍ]
>
> Actúa como Product Designer Senior. Basado en el contexto anterior, diseña la interfaz completa en Stitch:
> 1. **Branding Dinámico:** Diseña cómo el logo y colores cambian según el `tenant_id` en el dashboard.
> 2. **Admin Dashboard:** Layout de gestión de espacios (grid), calendario global de reservas y sección de facturación.
> 3. **Member Dashboard (Mobile First):** Interfaz enfocada en la reserva rápida mediante slots de tiempo y visualización de membresía activa.
> 4. **Componentes:** Diseña los Toasts de feedback, Skeletons de carga y el Toggle de Dark/Light mode (Slate-900 / Slate-50).
> **Entregable:** Prototipo visual de alta fidelidad que refleje la estética Linear/Icomat.

---

### PASO 2: Desarrollo Frontend & Estructura (Para ANTIGRAVITY)
*Este prompt toma el diseño y crea el cascarón funcional siguiendo las reglas técnicas.*

> **PROMPT 2: FRONTEND ARCHITECTURE & PWA**
> [PEGAR BLOQUE DE CONTEXTO AQUÍ]
>
> Actúa como Desarrollador Frontend Senior. Implementa la estructura del proyecto basada en el diseño de la etapa anterior:
> 1. **Estructura de Carpetas:** Crea `/admin` y `/member` con navegación independiente (Sidebar vs Bottom Tab Bar).
> 2. **Reglas Técnicas:** Configura el sistema de imports relativos y crea `src/data/mockData.ts` con los datos de los 2 tenants demo (Espacio Centro y WorkHub Norte).
> 3. **PWA:** Genera el `manifest.json` y el Service Worker básico para que la app sea instalable.
> 4. **UI:** Implementa los componentes de calendario, formularios de CRUD y el sistema de Toasts reactivos con Framer Motion.
> **Entregable:** Repositorio base con layouts funcionales y navegación lista.

---

### PASO 3: Base de Datos y Seguridad (Para SUPABASE)
*Aquí es donde creamos el motor y los muros de seguridad de los datos.*

> **PROMPT 3: BACKEND, RLS & DATA MODEL**
> [PEGAR BLOQUE DE CONTEXTO AQUÍ]
>
> Actúa como Arquitecto de Datos. Configura el backend en Supabase mediante MCP:
> 1. **Esquema SQL:** Crea las 8 tablas definidas en el contexto, asegurando relaciones correctas (Foreign Keys).
> 2. **Multi-tenancy RLS:** Redacta las políticas de Row Level Security para que TODO filtro dependa del `auth.jwt() -> 'tenant_id'`. Un usuario de un coworking jamás debe ver datos de otro.
> 3. **Auth Hooks:** Crea un trigger para que, al registrar un usuario, se cree automáticamente su entrada en `profiles`.
> 4. **Seed Data:** Inserta los datos de prueba para los 2 tenants demo (Admin + 2 Miembros cada uno) para testing inmediato.
> **Entregable:** Script SQL completo y configuración de tablas en Supabase.

---

### PASO 4: Lógica de Negocio e Integración (Para FINAL DEVS)
*El paso final para que la app "piense" y se conecte a los subdominios.*

> **PROMPT 4: BUSINESS LOGIC & TENANT ROUTING**
> [PEGAR BLOQUE DE CONTEXTO AQUÍ]
>
> Actúa como Lead Fullstack. Finaliza la integración del sistema:
> 1. **Detección de Subdominio:** Implementa la lógica para que `tenant-slug.tucowork.com` cargue la configuración de branding de ese tenant desde la tabla `tenants`.
> 2. **Lógica de Reservas:** Programa las validaciones: 
>    - Impedir reservas que no respeten la anticipación mínima (ej: 24h).
>    - Evitar solapamientos de horario en el mismo `space_id`.
> 3. **Dashboard de Miembro:** Conecta la vista de "Mi Membresía" y el historial de pagos con los datos reales de Supabase.
> 4. **Funciones Extra:** Implementa la exportación a CSV para el admin y la generación dinámica de códigos QR para check-in.
> **Entregable:** Aplicación SaaS 100% funcional y conectada.
