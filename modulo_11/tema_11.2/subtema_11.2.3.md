# Subtema 11.2.3: Caching de Herramientas Costosas

Si tu herramienta `analyze_huge_dataset` tarda 30 segundos y cuesta $0.50 en API calls, necesitas caché.

## Estrategias

1.  **In-Memory (LRU):** Rápido, local al proceso. Se pierde al reiniciar.
2.  **Distribuido (Redis):** Persistente y compartido entre réplicas.

## Decorador de Caching (Concepto)

```python
import functools

# Cache simple en memoria para demostración
@functools.lru_cache(maxsize=128)
def expensive_operation(param):
    return remote_api.call(param)

@mcp.tool()
def get_data(id: str):
    return expensive_operation(id)
```

**Ojo con la seguridad:** No cachees datos sensibles si no puedes garantizar aislamiento entre usuarios (multitenancy).
