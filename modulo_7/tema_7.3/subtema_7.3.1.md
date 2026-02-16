# Subtema 7.3.1: ClientSession: Conexión y Ciclo de Vida

Para consumir servidores MCP desde Python, usamos `ClientSession`.

## Configuración del Transporte

El cliente necesita saber cómo hablar con el servidor. Usualmente usamos `stdio` para servidores locales.

```python
import asyncio
from mcp.client.stdio import stdio_client
from mcp.client.session import ClientSession

async def main():
    # Parámetros del servidor a ejecutar
    server_params = stdio_client.StdioServerParameters(
        command="python",
        args=["my_server.py"], # Ruta a tu servidor
        env=None # Variables de entorno opcionales
    )

    # Context Manager para el transporte stdio
    async with stdio_client(server_params) as (read_stream, write_stream):

        # Context Manager para la sesión MCP
        async with ClientSession(read_stream, write_stream) as session:

            # Inicializar conexión (handshake)
            await session.initialize()

            # Listar herramientas
            tools = await session.list_tools()
            print(f"Herramientas encontradas: {[t.name for t in tools.tools]}")

if __name__ == "__main__":
    asyncio.run(main())
```

El doble `async with` asegura que tanto el proceso hijo (`stdio`) como la sesión MCP se cierren limpiamente.
