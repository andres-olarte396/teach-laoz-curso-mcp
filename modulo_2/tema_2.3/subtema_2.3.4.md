# Subtema 2.3.4: Compatibilidad Retroactiva: Soporte Dual SSE y Streamable HTTP

No todos los clientes soportan Streamable HTTP todavía. Para maximizar la compatibilidad, un servidor MCP moderno debería soportar **ambos** transportes.

## Detección Automática (Content Negotiation)

Tu servidor puede inspeccionar los headers de la petición entrante para decidir qué transporte usar.

### Lógica de Decisión

1.  Si el Cliente hace **POST** y envía header `Upgrade: mcp`:
    -> Usar **Streamable HTTP**.

2.  Si el Cliente hace **GET** y acepta `text/event-stream`:
    -> Usar **SSE** (y esperar peticiones POST separadas en el endpoint de mensajes).

3.  Si es **stdin**:
    -> Usar transporte **stdio**.

Los SDKs oficiales de TypeScript y Python ya incluyen abstracciones (`McpServer`) que pueden configurarse para manejar múltiples transportes simultáneamente, facilitando esta tarea al desarrollador.
