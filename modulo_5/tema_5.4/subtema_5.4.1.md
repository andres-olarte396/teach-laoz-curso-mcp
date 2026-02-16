# Subtema 5.4.1: Logging Estructurado: notifications/message

Los `print()` a stderr son útiles para debugging rápido, pero MCP ofrece un mecanismo formal de logging que el Host puede estructurar, filtrar y mostrar en una interfaz dedicada.

## Niveles de Log

MCP define niveles estándar:

- `debug`: Información detallada para desarrolladores.
- `info`: Eventos normales del sistema.
- `notice`: Eventos importantes pero normales.
- `warning`: Algo anómalo pero recuperable.
- `error`: Fallo en una operación específica.
- `critical`: Fallo grave del sistema.
- `alert`: Acción inmediata requerida.
- `emergency`: Sistema inutilizable.

## Envíando Logs

```json
{
  "method": "notifications/message",
  "params": {
    "level": "warning",
    "data": {
      "message": "Conexión a DB lenta",
      "latency_ms": 1500,
      "query_id": "qp-99"
    },
    // Opcional: logger name
    "logger": "db-pool"
  }
}
```

El Host recibe esto y puede decidir mostrar un icono amarillo de advertencia, o ignorarlo si está configurado en modo "solo errores".
