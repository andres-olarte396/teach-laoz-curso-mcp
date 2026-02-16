# Subtema 13.1.1: Glosario de Términos MCP

Definiciones rápidas para refrescar la memoria.

## Core

- **MCP (Model Context Protocol):** Estándar abierto para conectar IAs con datos y herramientas.
- **Host:** La aplicación que controla el LLM y la UI (ej: Claude Desktop, Cursor, IDEs). Es el "Cliente MCP".
- **Server:** Proceso que expone capacidades (Tools, Resources, Prompts) al Host.
- **Client:** Librería dentro del Host que habla el protocolo MCP.

## Primitivas

- **Tool:** Función ejecutable por el LLM. Puede tener efectos secundarios (side-effects).
- **Resource:** Datos pasivos (archivos, logs, DB rows) que el LLM puede leer como contexto.
- **Resource Template:** Patrón URI (ej: `logs://{id}`) para definir recursos dinámicos.
- **Prompt:** Plantilla de mensaje predefinida que el usuario puede invocar desde la UI del Host.
- **Sampling:** Capacidad del Servidor para pedirle al Host que complete un texto usando su LLM (Human-in-the-loop inverso).

## Transporte

- **Stdio Transport:** Comunicación mediante pipes (stdin/stdout). Ideal para procesos locales.
- **SSE Transport:** Server-Sent Events sobre HTTP. Para conexiones remotas.
- **JSON-RPC 2.0:** Formato de mensaje usado por MCP (Requests, Notifications, Errors).
