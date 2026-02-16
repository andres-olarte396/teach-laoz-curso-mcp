# Subtema 7.2.1: Lifespan: Gestión de Recursos del Servidor

Cuando tu servidor arranca, a menudo necesitas conectar a una base de datos o cargar un modelo de ML. No quieres hacer esto en cada llamada a una tool.

FastMCP usa el patrón `lifespan` (context manager) para esto.

## Definición del Context Manager

```python
from fastmcp import FastMCP
from contextlib import asynccontextmanager

# Estado global (o mejor, inyectado)
db_pool = {}

@asynccontextmanager
async def server_lifespan(server: FastMCP):
    # --- Startup ---
    print("Conectando a DB...")
    db_pool["connection"] = "ACTIVE"

    yield # Aquí el servidor corre y atiende peticiones

    # --- Shutdown ---
    print("Cerrando DB...")
    db_pool.clear()

mcp = FastMCP("LifespanDemo", lifespan=server_lifespan)

@mcp.tool()
def query_db() -> str:
    if db_pool.get("connection") != "ACTIVE":
        return "Error: DB no conectada"
    return "Resultados de la DB..."
```

Esto garantiza una limpieza correcta de recursos cuando el servidor se detiene (ej: cuando cierras Claude Desktop).
