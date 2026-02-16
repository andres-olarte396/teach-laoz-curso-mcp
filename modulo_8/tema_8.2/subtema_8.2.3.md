# Subtema 8.2.3: Desarrollo de un Host MCP Personalizado

¿Quieres crear tu propio chat que use herramientas MCP?

## Cliente MCP Mínimo

Usando el SDK de TypeScript (`@modelcontextprotocol/sdk`), un "Host" es simplemente un Cliente que conecta la UI con el protocolo.

### Flujo

1.  **Inicialización:** El Host lee una config (como la de Claude) y lanza los subprocesos de los servidores.
2.  **User Input:** El usuario escribe "Suma 2+2".
3.  **LLM Call:** El Host envía el texto al LLM (ej: OpenAI GPT-4) junto con la definición de herramientas (obtenida vía `client.listTools()`).
4.  **Tool Call:** El LLM responde con un JSON pidiendo ejecutar `sumar(2, 2)`.
5.  **Ejecución:** El Host intercepta esto, busca el cliente MCP correcto, llama a `client.callTool(...)` y obtiene el resultado.
6.  **Respuesta Final:** El Host envía el resultado de la herramienta al LLM, que genera la respuesta final en lenguaje natural.

Construir tu propio Host te da control total sobre la UX, permisos y qué servidores se activan cuándo.
