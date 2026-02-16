# Subtema 6.4.3: Testing de Integración: End-to-End

Para validar que el servidor arranca correctamente como proceso independiente y se comunica por `stdio`.

## Ejemplo de Test E2E

Podemos usar el `Client` real con `StdioClientTransport`.

```typescript
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";
import { Client } from "@modelcontextprotocol/sdk/client/index.js";

// Este test asume que ya has hecho 'npm run build'
test("Servidor real responde por stdio", async () => {
  const transport = new StdioClientTransport({
    command: "node",
    args: ["dist/index.js"],
  });

  const client = new Client(
    { name: "e2e-client", version: "1.0" },
    { capabilities: {} },
  );

  try {
    await client.connect(transport);

    // Verificar que lista herramientas
    const tools = await client.listTools();
    expect(tools.tools.length).toBeGreaterThan(0);
  } finally {
    // Importante: cerrar para matar el subproceso
    await client.close();
  }
});
```

Este test verifica parsin de argumentos, variables de entorno y configuración de arranque real.
