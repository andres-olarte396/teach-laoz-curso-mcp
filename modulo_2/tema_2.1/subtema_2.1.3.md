# Subtema 2.1.3: Gestión de Procesos y Ciclo de Vida en stdio

Cuando configuras Claude Desktop para usar un servidor local, estás configurando un gestor de procesos.

## Configuración de Claude (`claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "mi-servidor-python": {
      "command": "python",
      "args": ["/ruta/absoluta/a/servidor.py"],
      "env": {
        "API_KEY": "secreto"
      }
    },
    "mi-servidor-node": {
      "command": "node",
      "args": ["/ruta/absoluta/a/build/index.js"]
    }
  }
}
```

## Ciclo de Vida del Proceso

1.  **Spawn:** Cuando abres Claude, él lee la config y ejecuta (`spawn`) el comando especificado.
2.  **Comunicación:** Claude conecta pipes a stdin/stdout del proceso hijo.
3.  **Logs:** Claude captura stderr y lo guarda en sus logs (útil para debug).
4.  **Muerte (Kill):** Cuando cierras Claude, él envía una señal `SIGTERM` al proceso hijo.

### Manejo de SIGTERM / SIGINT

Tu servidor debe ser capaz de cerrar ordenadamente.

**En Python:**

```python
import signal
import sys

def handle_sigterm(signum, frame):
    sys.stderr.write("Recibido SIGTERM, cerrando conexiones...\n")
    # Cerrar DB, limpiar archivos temp, etc.
    sys.exit(0)

signal.signal(signal.SIGTERM, handle_sigterm)
```

**En Node.js:**

```javascript
process.on("SIGTERM", () => {
  console.error("Recibido SIGTERM, cerrando...");
  process.exit(0);
});
```

Si tu servidor no responde a SIGTERM en unos segundos, el Host enviará `SIGKILL` (apagado forzado).
