# Subtema 2.1.2: Implementación de un Servidor stdio Desde Cero

Vamos a construir un servidor MCP minimalista que funcione sobre stdio sin usar SDKs, para entender la "magia".

## Ejemplo en Python

Este script lee líneas de stdin, parsea el JSON, y si es un "ping", responde "pong".

```python
import sys
import json

def main():
    # Escribimos a stderr para no romper el protocolo
    sys.stderr.write("Servidor MCP iniciado en stdio...\n")
    sys.stderr.flush()

    for line in sys.stdin:
        try:
            request = json.loads(line)

            # Verificar versión JSON-RPC (simplificado)
            if request.get("jsonrpc") != "2.0":
                continue

            # Manejar 'initialize' (Obligatorio para que Claude conecte)
            if request.get("method") == "initialize":
                response = {
                    "jsonrpc": "2.0",
                    "id": request["id"],
                    "result": {
                        "protocolVersion": "2024-11-05",
                        "capabilities": {},
                        "serverInfo": {"name": "demo-stdio", "version": "1.0"}
                    }
                }

            # Manejar 'ping'
            elif request.get("method") == "ping":
                response = {
                    "jsonrpc": "2.0",
                    "id": request["id"],
                    "result": {}
                }

            # Cualquier otra cosa
            else:
                # Ignoramos para simplificar, o devolvemos error
                continue

            # ENVIAR RESPUESTA
            # json.dumps crea el string, print añade el \n final
            print(json.dumps(response))
            sys.stdout.flush() # Importante: asegurar que se envía inmediatamente

        except json.JSONDecodeError:
            sys.stderr.write("Error: JSON inválido recibido\n")

if __name__ == "__main__":
    main()
```

## Probando el Servidor

Puedes probar esto directamente en tu terminal usando pipes:

```bash
# Crear un archivo request.json
echo '{"jsonrpc": "2.0", "method": "initialize", "params": {...}, "id": 1}' > request.json

# Ejecutar
cat request.json | python servidor.py
```

Deberías ver la respuesta JSON en tu terminal.
