# SECUENCIA DE SPRINTS — BACKEND COWORKING SAAS

## SPRINT 1: Esquema y Auth
**Prompt:**
> "Usa `@file` como referencia.
> Genera el SQL para crear todas las tablas del sistema de coworking
> con sus tipos de datos, foreign keys y constraints.
> Incluye el trigger `on_auth_user_created` que inserte automáticamente
> en `profiles` al registrar un usuario en Supabase Auth, tomando
> `tenant_id`, `full_name` y `role` desde los metadatos del signup.
> No actives RLS todavía. Usa el MCP de Supabase para aplicarlo directamente.
> Variables de entorno en `.env`."

## SPRINT 2: Multitenancy — JWT Hook
**Prompt:**
> "Crea el hook `custom_access_token_hook` en Supabase.
> La función debe leer el `tenant_id` y el `role` del perfil del usuario
> e inyectarlos como claims en el JWT en cada login.
> Actívalo desde Authentication > Hooks en el dashboard.
> Este claim será la base de toda la seguridad RLS."

## SPRINT 3: Blindaje RLS
**Prompt:**
> "Activa RLS en todas las tablas y crea las políticas de seguridad:
> 1. Todo acceso se filtra por `auth.jwt()->>'tenant_id'`. Un usuario
>    nunca puede ver datos de otro tenant bajo ninguna circunstancia.
> 2. Los miembros ven y gestionan solo sus propias reservas, membresías
>    y pagos. Pueden cancelar pero no borrar.
> 3. Los miembros ven todos los spaces y anuncios publicados de su tenant.
> 4. Los admins tienen acceso total (ALL) a todas las tablas de su tenant.
> Usa el MCP de Supabase para aplicarlo."

## SPRINT 4: Seed Data
**Prompt:**
> "Inserta los datos de prueba para los 2 tenants demo definidos
> en @00.supabase.blueprint.md (Espacio Centro y WorkHub Norte).
> Crea sus spaces, un admin y dos miembros por tenant.
> El script debe ser idempotente (ON CONFLICT DO NOTHING).
> Usa el MCP de Supabase para aplicarlo."

## SPRINT 5: Integración Frontend
**Prompt:**
> "Configura el cliente `supabase-js` en el frontend Vue.js.
> Reemplaza todos los datos de `mockData.ts` por queries reales
> a Supabase usando el cliente autenticado.
> Implementa el flujo de signup pasando `tenant_id`, `full_name`
> y `role` en `options.data` para que el trigger los capture.
> Conecta la lista de reservas con una suscripción Realtime
> para que los cambios se reflejen sin recargar la página."

## SPRINT 6: Edge Function — Validación de Reservas
**Prompt:**
> "Implementa la Edge Function `validate-booking` en Deno.
> Debe recibir `space_id`, `starts_at` y `ends_at`, verificar que
> no haya solapamiento de horarios en la tabla `reservations`,
> insertar la reserva si es válida usando el Service Role Key,
> y retornar un error descriptivo si el horario está ocupado.
> Conéctala al formulario de reserva del frontend y muestra
> los errores en la UI mediante el sistema de Toasts existente."