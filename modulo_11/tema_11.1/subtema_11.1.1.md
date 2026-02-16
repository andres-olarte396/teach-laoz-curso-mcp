# Subtema 11.1.1: Logging Estructurado

En producción, `console.log` no es suficiente. Necesitas logs que una máquina pueda indexar.

## JSON Logs

Configura tu logger (Winster en Node, structlog en Python) para emitir JSON.

```json
{
  "level": "info",
  "timestamp": "2023-10-27T10:00:00Z",
  "service": "weather-mcp",
  "requestId": "req-123",
  "tool": "get_weather",
  "params": { "city": "Madrid" },
  "message": "Tool execution started"
}
```

## Correlation IDs

El objeto `requestContext` de MCP (y `RequestHeaderExtra` en TS) suele proveer un ID de petición. Pásalo en todos tus logs para trazar una operación desde el Host hasta la base de datos.
