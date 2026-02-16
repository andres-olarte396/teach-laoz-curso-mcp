# Subtema 11.1.2: Métricas: Latencia y Errores

Lo que no se mide, no se puede mejorar.

## Métricas Clave (RED Method)

1.  **Rate:** Peticiones por segundo (RPM) por herramienta.
2.  **Errors:** % de llamadas que fallan o lanzan excepciones.
3.  **Duration:** Latencia (p50, p95, p99) de cada ejecución de herramienta.

## Implementación con OpenTelemetry

EL SDK de MCP no emite métricas automáticamente aún, pero puedes envolver tus handlers.

```python
# Python con Prometheus Client
from prometheus_client import Summary
REQUEST_TIME = Summary('mcp_tool_processing_seconds', 'Time spent processing tool', ['tool_name'])

@mcp.tool()
@REQUEST_TIME.labels(tool_name='my_tool').time()
def my_tool():
    ...
```

Esto permite exportar datos a Grafana para visualizar "Qué herramientas son las más lentas".
