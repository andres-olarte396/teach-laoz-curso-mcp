# Subtema 7.1.3: Manejo de Tipos Complejos con Pydantic

Para argumentos más complejos que un `int` o `str`, FastMCP se integra nativamente con **Pydantic**.

## Modelos como Argumentos

```python
from fastmcp import FastMCP
from pydantic import BaseModel, Field

mcp = FastMCP("TiendaServer")

class Producto(BaseModel):
    nombre: str = Field(description="Nombre del producto")
    precio: float = Field(description="Precio en USD", gt=0)
    tags: list[str] = []

@mcp.tool()
def crear_producto(producto: Producto) -> str:
    """Registra un nuevo producto en el inventario."""
    # Aquí 'producto' ya es una instancia validada de la clase Producto
    return f"Producto {producto.nombre} creado con precio ${producto.precio}"
```

El LLM recibirá un esquema JSON detallado incluyendo las validaciones (como `gt=0` para precio positivo), lo que reduce drásticamente los errores de alucinación en los argumentos.
