# Subtema 10.3.1: MCP Server Registry

El protocolo es tan útil como las herramientas disponibles. Existe un registro oficial de servidores comunitarios.

## Usando el Registro

Puedes explorar `github.com/modelcontextprotocol/servers` para encontrar cientos de implementaciones listas para usar.

### Categorías Populares

- **Filesystem / Git:** Para manipular código.
- **Database:** PostgreSQL, SQLite.
- **Browser:** Puppeteer para navegar la web.
- **API Wrappers:** Slack, GitHub, Linear, Google Drive.

## Instalación

La mayoría se instalan con `uv` o `npx` directamente en tu config de Claude Desktop.

```json
"filesystem": {
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/me/Desktop"]
}
```
