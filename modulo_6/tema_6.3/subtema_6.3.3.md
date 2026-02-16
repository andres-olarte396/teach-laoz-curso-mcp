# Subtema 6.3.3: Cliente Multi-Servidor: Conexión Simultánea

Un Host real (como Claude Desktop) no se conecta a un solo servidor; se conecta a **muchos**.

## Patrón de Agregación

No existe una clase "MultiClient" en el SDK. Tienes que gestionar una colección de clientes.

```typescript
class MultiServerClient {
  private clients: Client[] = [];

  async addServer(command: string, args: string[]) {
    const transport = new StdioClientTransport({ command, args });
    const client = new Client(
      { name: "hub", version: "1.0" },
      { capabilities: {} },
    );
    await client.connect(transport);
    this.clients.push(client);
  }

  async getAllTools() {
    // Agregar herramientas de todos los clientes
    const allTools = [];
    for (const client of this.clients) {
      const tools = await client.listTools();
      allTools.push(...tools.tools.map((t) => ({ ...t, _clientId: client })));
    }
    return allTools;
  }

  async callTool(name: string, args: any) {
    // Encontrar qué cliente tiene esta herramienta
    // (Simplificado: asume nombres únicos)
    const client = this.findClientForTool(name);
    return client.callTool({ name, arguments: args });
  }
}
```

## Retos del Multi-Servidor

1.  **Colisión de Nombres:** ¿Qué pasa si dos servidores tienen una herramienta llamada `read_file`? (Solución: Namespacing visual o prefijos).
2.  **Ciclo de Vida:** Si un servidor crashea, no debe tirar abajo todo el Host.
