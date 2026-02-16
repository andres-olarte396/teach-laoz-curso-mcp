# Subtema 0.3.3: Primer Contacto con Claude Desktop y MCP Inspector

## Configurando Claude Desktop

Claude Desktop lee su configuración de un archivo JSON.

- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

Si el archivo no existe, deberás crearlo. Aquí es donde registraremos nuestros servidores MCP.

## MCP Inspector

El **MCP Inspector** es una herramienta de desarrollo web que te permite probar tus servidores MCP sin necesidad de Claude Desktop. Es ideal para depurar.

### Uso Básico

```bash
npx @modelcontextprotocol/inspector <comando_para_ejecutar_tu_servidor>
```

Por ejemplo, si tienes un servidor en python:

```bash
npx @modelcontextprotocol/inspector python main.py
```

Esto abrirá una interfaz web en `localhost:5173` donde podrás ver:

- Lista de herramientas disponibles.
- Recursos.
- Prompts.
- Logs de la comunicación JSON-RPC en tiempo real.
