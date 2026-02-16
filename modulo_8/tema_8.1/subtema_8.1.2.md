# Subtema 8.1.2: Debugging: Logs, Errores Comunes y Resolución

Cuando conectas un servidor y "no pasa nada" (el icono del enchufe no aparece o sale error), necesitas depurar.

## Ver los Logs

Claude Desktop guarda logs de MCP.

1.  En macOS: `tail -f ~/Library/Logs/Claude/mcp.log`
2.  En Windows: `%APPDATA%\Claude\logs\mcp*.log`

## Errores Comunes

### 1. "Connection refused" / "Command not found"

- **Causa:** La ruta al ejecutable (`node`, `python`, `uv`) no está en el PATH del entorno de Claude.
- **Solución:** Usa la ruta absoluta al ejecutable (e.g., `C:\Program Files\nodejs\node.exe`).

### 2. El servidor arranca pero se cierra inmediatamente

- **Causa:** Error de sintaxis en tu código o falta una librería.
- **Solución:** Prueba a ejecutar el comando `command + args` manualmente en tu terminal para ver el traceback.

### 3. "SyntaxError: Unexpected token"

- **Causa:** Tu servidor imprimió algo en `stdout` que NO era un mensaje JSON-RPC (ej: un `console.log("Hola")`).
- **Solución:** Todos los logs de depuración deben ir a `stderr`. Usa `console.error()` en JS o `print(..., file=sys.stderr)` en Python.
