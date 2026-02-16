# Subtema 2.2.1: Server-Sent Events: Fundamentos y Flujo Unidireccional

## ¿Qué es SSE?

**Server-Sent Events (SSE)** es un estándar HTML5 que permite a un servidor web enviar actualizaciones a una página web de forma asíncrona, en tiempo real, sobre una conexión HTTP única.

A diferencia de WebSockets (que es bidireccional puro), SSE es **unidireccional**: solo del servidor al cliente.

## Formato del Mensaje SSE

SSE es texto plano. Cada mensaje comienza con `data:` y termina con dos saltos de línea.

```text
data: {"jsonrpc": "2.0", "method": "notifications/message", "params": {...}}

data: {"jsonrpc": "2.0", "result": "ok", "id": 1}

```

También soporta eventos nombrados y IDs:

```text
event: message
id: 123
data: contenido del mensaje
```

## SSE en MCP

En MCP, usamos SSE para simular la mitad del canal bidireccional.

- El **Cliente** se suscribe a un endpoint (ej: `/sse`) mediante una petición GET.
- El **Servidor** mantiene esa conexión abierta y envía mensajes JSON-RPC a través de ella.
- Estos mensajes son **del Servidor hacia el Cliente** (Respuestas y Notificaciones).

Pero, ¿cómo envía el Cliente mensajes al Servidor (Peticiones)? SSE no permite enviar datos.
Por eso necesitamos una **Arquitectura Dual**.
