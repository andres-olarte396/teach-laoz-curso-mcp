# Subtema 8.1.1: Configuración de claude_desktop_config.json

![Claude Desktop Config](../../../diagramas/modulo_8/claude_desktop_config.svg)

Claude Desktop es actualmente el host (cliente) más popular para MCP. Permite a Claude interactuar con tus herramientas locales.

## Ubicación del Archivo

Dependiendo de tu SO, el archivo de configuración está en:

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

## Estructura

El archivo define un mapa de servidores bajo la clave `mcpServers`.

```json
{
  "mcpServers": {
    "mi-servidor-local": {
      "command": "node",
      "args": ["/Users/andres/repos/mi-server/dist/index.js"],
      "env": {
        "API_KEY": "secret_123"
      }
    },
    "mi-servidor-python": {
      "command": "uv",
      "args": ["--directory", "/Users/andres/repos/py-server", "run", "main.py"]
    }
  }
}
```

> **Nota:** Siempre usa rutas absolutas para evitar problemas.

