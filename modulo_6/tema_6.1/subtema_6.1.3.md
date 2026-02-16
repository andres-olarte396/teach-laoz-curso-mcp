# Subtema 6.1.3: Server: La API de Bajo Nivel y Request Handlers

A veces `McpServer` es "demasiado mágico". Si necesitas control total sobre cada mensaje o estás implementando características experimentales, usa la clase base `Server`.

## Implementación Manual

```typescript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import {
  CallToolRequestSchema,
  ListToolsRequestSchema,
  ErrorCode,
  McpError,
} from "@modelcontextprotocol/sdk/types.js";

// 1. Instancia base
const server = new Server(
  {
    name: "low-level-server",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {}, // Declaramos explícitamente qué soportamos
    },
  },
);

// 2. Handler para Listar Herramientas
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return {
    tools: [
      {
        name: "echo",
        description: "Repite lo que dices",
        inputSchema: {
          type: "object",
          properties: {
            message: { type: "string" },
          },
        },
      },
    ],
  };
});

// 3. Handler para Llamar Herramientas
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  if (request.params.name === "echo") {
    const msg = String(request.params.arguments?.message);
    return {
      content: [{ type: "text", text: `Echo: ${msg}` }],
    };
  }

  throw new McpError(ErrorCode.MethodNotFound, "Herramienta no encontrada");
});

// 4. Conectar
const transport = new StdioServerTransport();
await server.connect(transport);
```

## Diferencias Clave

- **Verbosity:** Tienes que definir los handlers `ListTools` y `CallTool` por separado.
- **Control:** Puedes insertar lógica de autenticación o logging customizado dentro de cada handler.
- **Esquemas:** Debes escribir el JSON Schema manualmente (o generarlo tú mismo), `McpServer` no lo hace por ti aquí.
