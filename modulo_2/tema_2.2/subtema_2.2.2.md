# Subtema 2.2.2: Arquitectura Dual: Endpoint SSE + Endpoint POST

Para lograr comunicación bidireccional completa sobre HTTP (versión legacy o simple), MCP utiliza dos endpoints separados.

## 1. El Endpoint SSE (`GET /sse`)

- El cliente abre una conexión `GET` persistente.
- El servidor responde con `Content-Type: text/event-stream`.
- A través de este canal, el servidor envía mensajes JSON-RPC al cliente.

**Crucial:** El primer mensaje que envía el servidor por este canal **debe ser la URI del endpoint POST**.

```text
event: endpoint
data: /message?session_id=abc-123
```

## 2. El Endpoint POST (`POST /message`)

- Cuando el cliente quiere enviar un mensaje (ej: `tools/call`), hace una petición `POST` estándar a la URL que recibió en el paso anterior.
- El cuerpo del POST es el mensaje JSON-RPC.
- El servidor procesa el mensaje y, si hay respuesta, **la envía por el canal SSE**, no como respuesta al POST (típicamente el POST responde con `202 Accepted`).

## Diagrama de Flujo

1.  **Cliente:** `GET /sse`
2.  **Servidor:** `200 OK` (Stream abierto). Envía evento `endpoint: /message?id=1`.
3.  **Cliente:** Recibe endpoint.
4.  **Cliente:** `POST /message?id=1` con cuerpo `{"method": "initialize"}`.
5.  **Servidor:** Recibe POST. Procesa initialize.
6.  **Servidor:** Envía por el stream SSE: `data: {"result": {"capabilities": ...}}`.

Esta arquitectura permite simular un socket bidireccional usando HTTP estándar sin WebSockets.
