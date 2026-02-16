# Subtema 6.3.1: Client: Conexión, Inicialización y Descubrimiento

Crear un Cliente MCP es necesario si estás construyendo tu propio IDE, Chatbot o Agente Orquestador.

## Conectando a un Servidor

Necesitamos la clase `Client` y un transporte de cliente (`StdioClientTransport` o `SSEClientTransport`).

```typescript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StdioClientTransport } from "@modelcontextprotocol/sdk/client/stdio.js";

// 1. Configurar el transporte (ej: lanzar un subproceso python)
const transport = new StdioClientTransport({
  command: "python",
  args: ["path/to/server.py"],
});

// 2. Crear instancia del cliente
const client = new Client(
  {
    name: "mi-cliente-ts",
    version: "1.0.0",
  },
  {
    capabilities: {
      prompts: {},
      resources: {},
      tools: {},
    },
  },
);

// 3. Conectar al transporte
await client.connect(transport);

// 4. Listar Herramientas Disponibles (Discovery)
const tools = await client.listTools();
console.log(
  "Herramientas encontradas:",
  tools.tools.map((t) => t.name),
);
```

El método `connect()` maneja automáticamente el handshake `initialize` y `notifications/initialized`.
