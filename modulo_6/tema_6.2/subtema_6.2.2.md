# Subtema 6.2.2: Registro Dinámico de Herramientas y Recursos

`McpServer` permite añadir capacidades después del inicio.

## Escenario: Plugins

Imagina que tu servidor detecta que el usuario instaló el plugin "Base de Datos". Quieres registrar las herramientas de base de datos en caliente.

```typescript
// Inicio normal
const server = new McpServer({ name: "dynamic-server", version: "1.0" });

// ... el servidor arranca ...

function onPluginLoaded(pluginName: string) {
  if (pluginName === "database") {

    // Registrar nueva herramienta dinámicamente
    server.tool(
      "query_db",
      "Ejecuta SQL",
      { sql: z.string() },
      async ({ sql }) => { return htmlResult(...) }
    );

    // CRÍTICO: Avisar a los clientes que la lista cambió
    // (Nota: McpServer hace esto automáticamente en versiones recientes,
    // pero si usas Server de bajo nivel, debes llamar a sendToolListChanged)
    console.log("Herramientas actualizadas, clientes notificados.");
  }
}
```

Esto permite arquitecturas modulares donde no todas las herramientas están cargadas en memoria desde el milisegundo cero.
