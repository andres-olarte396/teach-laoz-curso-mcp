# Subtema 7.1.2: FastMCP: Decoradores @tool, @resource y @prompt

![Decoradores FastMCP](../../../diagramas/modulo_7/fastmcp_decoradores.svg)

Si vienes de **FastAPI**, te sentirás en casa. `FastMCP` es una capa de alto nivel sobre el SDK base que usa **Type Hints** de Python para generar todo automáticamente.

## Hello World en Python

Crea `main.py`:

```python
from fastmcp import FastMCP

# 1. Crear la app

![Decoradores FastMCP](../../../diagramas/modulo_7/fastmcp_decoradores.svg)
mcp = FastMCP("DemoServer")

# 2. Definir una Tool

![Decoradores FastMCP](../../../diagramas/modulo_7/fastmcp_decoradores.svg)
@mcp.tool()
def sumar(a: int, b: int) -> int:
    """Suma dos números enteros."""
    return a + b

# 3. Definir un Resource Estático

![Decoradores FastMCP](../../../diagramas/modulo_7/fastmcp_decoradores.svg)
@mcp.resource("config://app")
def get_config() -> str:
    """Devuelve la configuración de la app."""
    return '{"version": "1.0", "env": "dev"}'

# 4. Definir un Prompt

![Decoradores FastMCP](../../../diagramas/modulo_7/fastmcp_decoradores.svg)
@mcp.prompt()
def revisar_codigo(codigo: str) -> str:
    """Crea un mensaje para revisar código."""
    return f"Por favor revisa este código buscando bugs:\n\n{codigo}"

# 5. Ejecutar

![Decoradores FastMCP](../../../diagramas/modulo_7/fastmcp_decoradores.svg)
if __name__ == "__main__":
    mcp.run()
```

## Magia Bajo el Capó

- Los argumentos `a: int, b: int` se convierten en un esquema JSON-RPC que el Host entiende.
- El docstring `"""Suma dos números..."""` se convierte en la descripción de la herramienta.
- `mcp.run()` detecta automáticamente si debe correr en modo stdio o SSE (según argumentos de línea de comandos).

