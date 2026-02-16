# Subtema 7.4.1: Testing con pytest y Fixtures

FastMCP facilita enormemente el testing porque podemos instanciar el servidor y llamar a las funciones decoradas directamente en unit tests, o usar clientes en memoria para tests de integración.

## Unit Testing Puro

Como `FastMCP` es Python estándar, puedes importar tus funciones y testearlas aisladamente si las desacoplas bien.

## Integration Testing (In-Memory)

```python
import pytest
from mcp.server.fastmcp import FastMCP
# Nota: La API exacta de test client puede variar según versión del SDK
# Aquí simulamos el patrón recomendado.

from my_server import mcp

@pytest.mark.asyncio
async def test_sumar_tool():
    # Arrancar servidor en modo test (sin stdio real)
    async with mcp.test_client() as client:
        result = await client.call_tool("sumar", arguments={"a": 1, "b": 2})
        assert result.content[0].text == "3"
```

## Mocking de Contexto

Si tu herramienta usa `ctx: Context`, necesitarás pasar un mock en tus tests.

```python
from unittest.mock import AsyncMock
from mcp.server.fastmcp import Context

async def test_tool_with_context():
    mock_ctx = AsyncMock(spec=Context)
    mock_ctx.info = AsyncMock()

    await mi_herramienta_con_contexto(mock_ctx)

    mock_ctx.info.assert_called_with("Iniciando...")
```
