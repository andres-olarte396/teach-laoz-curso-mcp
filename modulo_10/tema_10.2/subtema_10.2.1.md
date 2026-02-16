# Subtema 10.2.1: Agente Simple con Bucle Tool-Use

Un "Agente" no es más que un bucle `Pensar -> Actuar -> Observar`. MCP estandariza la parte de "Actuar".

## El Bucle ReAct con MCP

1.  **System Prompt:** "Eres un asistente útil. Tienes estas herramientas: [Lista devuelta por MCP client.listTools()]".
2.  **User Input:** "¿Cuál es el clima en Madrid?"
3.  **LLM:** "Pensamiento: Necesito saber el clima. Acción: weather_server.get_weather({city: 'Madrid'})".
4.  **Host (Tú):** Parsea la acción -> `mcpClient.callTool(...)` -> Obtiene "25°C".
5.  **Host:** Añade el resultado al historial: "Tool Output: 25°C".
6.  **LLM:** "El clima en Madrid es 25°C".

Al usar MCP, tu código de bucle no cambia si añades 1 o 100 herramientas nuevas.
