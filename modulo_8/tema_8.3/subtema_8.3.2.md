# Subtema 8.3.2: OpenAI Agents SDK con MCP

OpenAI también está apostando por agentes autónomos.

## Conexión

Aunque OpenAI usa su propio formato de `function calling` (JSON Schema), MCP es 100% compatible porque usa el mismo estándar.

Puedes escribir un pequeño adaptador que:

1.  Conecte al servidor MCP.
2.  Liste las herramientas (`list_tools`).
3.  Convierta el esquema MCP al formato de OpenAI `tools` parameter.
4.  Cuando el modelo devuelva `tool_calls`, invocar la herramienta MCP correspondiente.

Esto te permite usar servidores MCP con la API Assistants o con frameworks que consuman la API de OpenAI directamente.
