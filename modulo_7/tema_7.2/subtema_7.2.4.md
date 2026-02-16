# Subtema 7.2.4: Low-Level Server API: Handlers Manuales

Para cosas que FastMCP no cubra (como integraciones muy custom del protocolo), puedes bajar al nivel de `Server`.

## Implementación Base

La versión "low-level" en Python es `mcp.server.lowlevel`.

```python
import asyncio
from mcp.server.lowlevel import Server
from mcp.types import Tool, TextContent, ImageContent, EmbeddedResource

async def main():
    server = Server("low-level-py")

    @server.list_tools()
    async def list_tools() -> list[Tool]:
        return [
            Tool(name="echo", description="Echos input", inputSchema={...})
        ]

    @server.call_tool()
    async def call_tool(name: str, arguments: dict) -> list[TextContent | ImageContent | EmbeddedResource]:
        if name == "echo":
             return [TextContent(type="text", text=str(arguments))]
        raise ValueError("Unknown tool")

    # Ejecutar con stdio
    from mcp.server.stdio import stdio_server
    async with stdio_server() as streams:
        await server.run(streams[0], streams[1], server.create_initialization_options())

if __name__ == "__main__":
    asyncio.run(main())
```

Es más verboso que FastMCP, pero te da control total sobre el bucle de eventos asyncio y los streams de entrada/salida.
