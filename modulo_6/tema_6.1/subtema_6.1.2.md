# Subtema 6.1.2: McpServer: La API de Alto Nivel para Servidores

![McpServer vs Server](../../../diagramas/modulo_6/sdk_ts_arquitectura.svg)

La clase `McpServer` es la forma más rápida y segura de crear un servidor. Abstrae la gestión de conexiones y validación de tipos.

## Hello World en MCP

Crea `src/index.ts`:

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

// 1. Crear instancia del servidor
const server = new McpServer({
  name: "mi-servidor-demo",
  version: "1.0.0",
});

// 2. Registrar una Herramienta (Tool)
server.tool(
  "sumar",
  "Suma dos números",
  {
    a: z.number().describe("Primer número"),
    b: z.number().describe("Segundo número"),
  },
  async ({ a, b }) => {
    // La lógica de la herramienta
    return {
      content: [{ type: "text", text: String(a + b) }],
    };
  },
);

// 3. Iniciar el Transporte (stdio)
async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("Servidor MCP corriendo en stdio...");
}

main().catch((error) => {
  console.error("Error fatal:", error);
  process.exit(1);
});
```

## Explicación

1.  **`McpServer`**: Maneja el enrutado de JSON-RPC.
2.  **`server.tool()`**: Método helper que toma nombre, descripción, esquema (Zod) y callback. _¡Convierte Zod a JSON Schema automáticamente!_
3.  **`StdioServerTransport`**: Escucha en `stdin` y escribe en `stdout`.

## Ejecución

Para probarlo, compila y configura en Claude Desktop:

```bash
npm run build
# O usa tsx directamente

![McpServer vs Server](../../../diagramas/modulo_6/sdk_ts_arquitectura.svg)
npx tsx src/index.ts
```

