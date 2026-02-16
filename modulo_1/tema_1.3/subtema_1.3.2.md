# Subtema 1.3.2: Métodos del Protocolo MCP: El Catálogo Completo

MCP define un conjunto estándar de métodos JSON-RPC. Aquí están los más importantes agrupados por funcionalidad.

## Lifecycle (Ciclo de Vida)

- `initialize`: Handshake inicial.
- `notifications/initialized`: Confirmación de inicio.
- `ping`: Verificar latencia/conectividad.

## Tools (Herramientas)

- `tools/list`: Cliente pide lista de herramientas disponibles.
- `tools/call`: Cliente pide ejecutar una herramienta.
- `notifications/tools/list_changed`: Servidor avisa que hay nuevas herramientas.

## Resources (Recursos)

- `resources/list`: Listar recursos disponibles.
- `resources/read`: Leer contenido de un recurso.
- `resources/templates/list`: Listar plantillas de URI.
- `notifications/resources/list_changed`: Recursos cambiaron.
- `notifications/resources/updated`: Contenido de un recurso cambió.

## Prompts

- `prompts/list`: Listar prompts predefinidos.
- `prompts/get`: Obtener un prompt renderizado.

## Sampling (Muestreo / Completions)

- `sampling/createMessage`: **El servidor pide al cliente** que complete un mensaje usando el LLM (Human-in-the-loop o Chain-of-Thought implementado en servidor).
