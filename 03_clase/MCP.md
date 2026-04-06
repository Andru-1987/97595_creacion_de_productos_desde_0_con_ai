# ¿Qué es MCP?
> [MCP](https://blog.logto.io/es/que-es-mcp)

MCP (Protocolo de Contexto del Modelo) es un protocolo abierto y universal que estandariza cómo las aplicaciones proporcionan información de contexto a los modelos de lenguaje grandes (LLMs).

En pocas palabras, al igual que el protocolo HTTP permite que diferentes sitios web y navegadores intercambien información según las mismas reglas, MCP es como el protocolo HTTP del mundo de la IA. MCP permite que diferentes modelos de IA se conecten a varias fuentes de datos y herramientas de una manera estandarizada. Esta estandarización facilita a los desarrolladores construir aplicaciones de IA sin tener que crear interfaces especializadas para cada modelo o fuente de datos.


## Antigravity --> SupaBase MCP


- **Objetivo**: Facilitar la interacción con el servidor MCP directamente desde el entorno de desarrollo.
- **Ventajas**: Simplifica la configuración y permite pruebas rápidas de los modelos de IA.
- **Requisitos**: Tener una cuenta en Supabase y el token de acceso configurado.
- Steps directamente en el entorno


## VSCode --> SupaBase MCP

- **Configuración**: Añade el archivo `.vscode/mcp.json` para que VSCode reconozca el servidor.
- **Uso**: Permite lanzar prompts a tu modelo directamente desde el editor.
- **Ejemplo**: Ver el bloque JSON a continuación para la configuración básica.

- .vscode/mcp.json`

```json
{
  "servers": {
    "supabase": {
      "type": "http",
      "url": "https://mcp.supabase.com/mcp"
    }
  }
}
```

## Github --> MCP

- **Integración**: Conecta tu repositorio de GitHub con el servidor MCP para obtener sugerencias de código basadas en IA.
- **Pasos**: Sigue la guía oficial de GitHub Copilot para habilitar el MCP.
- **Beneficio**: Mejora la productividad al recibir recomendaciones contextuales mientras codificas.
[MCP GITHUB](https://docs.github.com/en/copilot/how-tos/provide-context/use-mcp/set-up-the-github-mcp-server)


