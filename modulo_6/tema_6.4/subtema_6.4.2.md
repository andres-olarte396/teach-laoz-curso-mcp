# Subtema 6.4.2: Testing Unitario: InMemoryTransport

Para tests unitarios, no queremos lanzar subprocesos reales. El SDK provee `InMemoryTransport` para conectar cliente y servidor en el mismo proceso de memoria.

## Setup con Vitest/Jest

```typescript
import { describe, it, expect, beforeEach, afterEach } from "vitest";
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import {
  InMemoryServerTransport,
  InMemoryClientTransport,
} from "@modelcontextprotocol/sdk/inMemory.js";
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { z } from "zod";

describe("Mi Servidor MCP", () => {
  let server: McpServer;
  let client: Client;

  beforeEach(async () => {
    // 1. Configurar Servidor
    server = new McpServer({ name: "test-server", version: "1.0" });
    server.tool(
      "sum",
      "Suma",
      { a: z.number(), b: z.number() },
      async ({ a, b }) => ({
        content: [{ type: "text", text: String(a + b) }],
      }),
    );

    // 2. Crear par de transportes conectados
    const [serverTransport, clientTransport] =
      InMemoryServerTransport.createLinkedPair();

    // 3. Conectar Servidor
    await server.connect(serverTransport);

    // 4. Conectar Cliente
    client = new Client(
      { name: "test-client", version: "1.0" },
      { capabilities: {} },
    );
    await client.connect(clientTransport);
  });

  afterEach(async () => {
    await server.close();
    await client.close();
  });

  it("debería sumar dos números correctamente", async () => {
    const result = await client.callTool({
      name: "sum",
      arguments: { a: 5, b: 3 },
    });

    expect(result.content[0].text).toBe("8");
  });
});
```

Esto ejecuta los tests en milisegundos, sin I/O real.
