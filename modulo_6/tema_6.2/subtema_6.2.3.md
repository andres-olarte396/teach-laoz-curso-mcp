# Subtema 6.2.3: Integración con Frameworks Web: Express y Hono

Para producción, probablemente quieras exponer tu servidor MCP sobre **HTTP con SSE**, y quizás compartir puerto con una API REST existente.

## Ejemplo con Express

Necesitamos el `SSEServerTransport`.

```typescript
import express from "express";
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { SSEServerTransport } from "@modelcontextprotocol/sdk/server/sse.js";

const app = express();
const server = new McpServer({ name: "express-mcp", version: "1.0" });

// Definir herramientas...
server.tool("hello", "...", {}, async () => ({
  content: [{ type: "text", text: "Hi!" }],
}));

app.get("/sse", async (req, res) => {
  const transport = new SSEServerTransport("/messages", res);
  await server.connect(transport);

  // El transporte maneja mantener la conexión abierta
});

app.post("/messages", async (req, res) => {
  // Aquí necesitamos manejar el POST y pasarlo al transporte correspondiente.
  // Nota: La implementación de SSE en Express requiere gestionar
  // el mapping de sessionID a transporte manualmente o usar un adaptador.

  // Por simplicidad, el SDK provee helpers para esto,
  // o podemos usar Hono que tiene mejor soporte de streaming.
  res.status(501).send("Implementación compleja omitida por brevedad.");
});

app.listen(3000, () => console.log("SSE en http://localhost:3000/sse"));
```

> **Recomendación:** Para SSE, usar **Hono** o **FastAPI** (Python) es mucho más sencillo que Express debido a su manejo nativo de Streams estándar.
