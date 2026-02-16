# Subtema 6.2.1: Herramientas con Contexto: RequestHandlerExtra y Sesión

A veces una herramienta necesita saber **quién** la está llamando o necesita enviar mensajes de log/progreso de vuelta al cliente. Para esto inyectamos el contexto.

## Accediendo al `extra`

En `McpServer`, el último argumento de tu callback recibe un objeto `RequestHandlerExtra`.

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { z } from "zod";

const server = new McpServer({ name: "context-demo", version: "1.0" });

server.tool(
  "long_operation",
  "Operación que reporta progreso",
  { steps: z.number() },
  async ({ steps }, extra) => {
    // <--- Aquí está la magia

    // 1. Acceder al ID de la Petición
    console.log(`Procesando request ${extra.requestId}`);

    // 2. Reportar Progreso (usando el contexto de la conexión)
    // Nota: La API de alto nivel para progreso está en desarrollo,
    // pero podemos acceder al transporte subyacente si es necesario.

    // 3. Enviar Logs
    extra.server.sendLoggingMessage({
      level: "info",
      data: "Iniciando operación larga...",
    });

    return {
      content: [{ type: "text", text: "Operación completada" }],
    };
  },
);
```

## Datos de Sesión

Si usas un transporte persistente (como SSE), puedes asociar datos a la conexión.
El objeto `extra` suele contener una referencia a la conexión, donde puedes leer/escribir metadatos de sesión (ej: `userId`) si implementaste tu propia lógica de autenticación en el transporte.
