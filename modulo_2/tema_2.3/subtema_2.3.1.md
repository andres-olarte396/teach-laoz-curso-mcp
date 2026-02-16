# Subtema 2.3.1: Arquitectura de Streamable HTTP

## La Solución Moderna

Streamable HTTP es la evolución del transporte en MCP. En lugar de dos endpoints separados (SSE GET + POST), utiliza un enfoque unificado.

## Cómo Funciona

1.  **POST Único:** Todo sucede en una sola conexión HTTP POST a un endpoint (ej: `/mcp`).
2.  **Streaming Bidireccional:** El cuerpo de la petición y el cuerpo de la respuesta pueden ser streams continuos de datos.
3.  **JSON Lines:** El formato de intercambio es JSON Lines (cada línea es un mensaje JSON completo).

```text
POST /mcp HTTP/1.1
Content-Type: application/x-ndjson

{"jsonrpc": "2.0", "method": "initialize", ...}
{"jsonrpc": "2.0", "method": "tools/call", ...}

... (conexión abierta) ...
```

El servidor responde en el mismo stream:

```text
HTTP/1.1 200 OK
Content-Type: application/x-ndjson

{"jsonrpc": "2.0", "result": {...}}
{"jsonrpc": "2.0", "method": "notifications/message", ...}
```

## Beneficios

- **Simplicidad:** Un solo endpoint.
- **Firewall Friendly:** Solo necesitas permitir tráfico HTTPS saliente estándar.
- **Eficiencia:** Menos handshakes TCP/TLS.
