# Conexion con MCP Custom y Deploy

## Posthog
Pasos para activar en posthog connection con mcp: 
- Creacion de mcp con antigravity -> Pues no se encuentra de manera nativa.
`MCP Server` -> `Manage MCP Server` -> `View Raw Config`

```bash
# este comando es para poder darle el poder al proyecto 
# usando la herramienta de Node.js (javascript) para que se pueda conectar a hesta herramienta

npx @posthog/wizard mcp add
```
[Posthog MCP](https://posthog.com/docs/model-context-protocol)

```json
{
    "mcpServers": {
        "supabase-mcp-server": {
            "command": "npx",
            "args": [
                "-y",
                "@supabase/mcp-server-supabase@latest",
                "--access-token",
                "tu-token-supabase"
            ]
        },
        "posthog": {
            "type": "http",
            "serverUrl": "https://mcp.posthog.com/mcp?features=flags,insights,sql,dashboards,events,persons",
            "headers": {
                "Authorization": "Bearer phx_SOY_PERSONAL_TOKEN"
            },
            "disabledTools": [
                "docs-search"
            ]
        }
    }
}
```

### Validar que el mcp este disponible
```markdown
@posthog List all projects in my PostHog organization
```

*Cuando revisemos que el mcp este listo podremos instalar las herramientas de analitica que requiera para este proyecto*

```markdown

Instala PostHog en el proyecto.

Crea un servicio `src/lib/analytics.ts` que exporte funciones para registrar eventos:
- `trackEvent(eventName: string, properties?: object)`

Instrumenta los siguientes eventos en sus respectivos componentes/páginas:
1. `login_success` – cuando el usuario inicia sesión (desde el store de Zustand).
2. `dashboard_view` – al cargar la página del dashboard.
3. `reservation_created` – después de crear una reserva

Cada evento debe incluir propiedades relevantes: `tenant_slug`, `user_role`, `space_type` (si aplica), `timestamp`.

Asegura que no se disparen eventos duplicados (idempotencia del lado del cliente) y que los errores de red no rompan la UI.
```


`Tip: En este concepto de vibecoding la IA suele tomar atribuciones que no son las mejores, por lo tanto lo mejor es ser mucho mas directo`

```markdown
**TASK: Integrate PostHog analytics**

**Step 1 — Install**
```
npm install posthog-js
```

**Step 2 — Create `src/lib/analytics.ts`**

Implement exactly this interface, no more:

```ts
export function initAnalytics(): void
export function trackEvent(eventName: string, properties?: Record<string, unknown>): void
```

Rules for `trackEvent`:
- Deduplicate using a `Set<string>` keyed on `eventName + JSON.stringify(properties)` — reset the Set every 5 seconds
- Wrap every call in try/catch — errors must be silently swallowed, never thrown
- Every call must merge these base properties automatically: `tenant_slug`, `user_role`, `timestamp: new Date().toISOString()`

Call `initAnalytics()` once in the app entry point.

**Step 3 — Instrument these events. Touch only the files listed.**

| Event | File to edit | Trigger point |
|---|---|---|
| `login_success` | Zustand auth store | After successful login, include `user_role` |
| `dashboard_view` | Dashboard page component | On mount (`useEffect` with empty deps), include `tenant_slug` |
| `reservation_created` | Reservation form/handler | After confirmed API response, include `tenant_slug`, `space_type` |

**Constraints — do not deviate:**
- Do not create additional files beyond `src/lib/analytics.ts`
- Do not add PostHog calls anywhere other than the 3 locations above
- Do not modify any types, interfaces, or existing exports in touched files
- PostHog key goes in `.env` as `VITE_POSTHOG_KEY` — read it via `import.meta.env`
- Do not install any package other than `posthog-js`

**Done when:** all 3 events appear in PostHog Live Events with the correct properties.    

```
 
> Evita ambiguedades en los usos de los recursos de decisiones.

---
 
## Resend MCP
 
 ```json
 {
  "mcpServers": {
    "resend": {
      "command": "npx",
      "args": ["-y", "resend-mcp"],
      "env": {
        "RESEND_API_KEY": "re_xxxxxxxxx"
      }
    }
  }
}
 ```
 
 
 