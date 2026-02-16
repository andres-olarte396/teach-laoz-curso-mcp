# Subtema 3.3.3: Herramientas de Larga Duración y Reporte de Progreso

Algunas herramientas tardan mucho (ej: "Analizar repositorio de 1GB", "Entrenar modelo"). Si el servidor no responde en ~60 segundos, el Host suele dar timeout.

## Notificaciones de Progreso

MCP permite reportar progreso mientras la herramienta se ejecuta.

```json
{
  "jsonrpc": "2.0",
  "method": "notifications/progress",
  "params": {
    "progressToken": "token-123", // Enviado por el cliente en tools/call
    "progress": 50,
    "total": 100
  }
}
```

## Implementación

El cliente debe iniciar la llamada incluyendo un `progressToken`. Si no lo incluye, no debes enviar progreso.

```python
@mcp.tool()
async def long_task(ctx: Context):
    for i in range(10):
        await sleep(1)
        await ctx.report_progress(i, 10)

    return "Tarea completada"
```

Esto mantiene la conexión viva y mejora la experiencia de usuario (barra de progreso en Claude Desktop).
