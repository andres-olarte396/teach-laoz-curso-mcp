# Subtema 13.2.1: Cheat Sheet de Desarrollo

## Python (FastMCP)

```python
from fastmcp import FastMCP

# 1. Crear servidor
mcp = FastMCP("MyServer")

# 2. Definir Tool
@mcp.tool()
def sumar(a: int, b: int) -> int:
    """Suma dos números."""
    return a + b

# 3. Definir Resource
@mcp.resource("config://app")
def get_config() -> str:
    return "DEBUG=True"

# 4. Ejecutar
if __name__ == "__main__":
    mcp.run()
```

## TypeScript (SDK)

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

// 1. Crear servidor
const server = new McpServer({ name: "MyServer", version: "1.0.0" });

// 2. Definir Tool
server.tool("sumar", { a: z.number(), b: z.number() }, async ({ a, b }) => ({
  content: [{ type: "text", text: String(a + b) }],
}));

// 3. Ejecutar
const transport = new StdioServerTransport();
await server.connect(transport);
```

## Comandos Útiles

- **Inspector:** `npx @modelcontextprotocol/inspector <command> <args>`
- **Instalar Servidor Filesystem:** `npx -y @modelcontextprotocol/server-filesystem /path`
