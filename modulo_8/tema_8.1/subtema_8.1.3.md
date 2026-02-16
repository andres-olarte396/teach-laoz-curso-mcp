# Subtema 8.1.3: Servidores Remotos en Claude Desktop

Aunque Claude Desktop está diseñado para "local-first", puede conectarse a servidores remotos usando un **Bridge** o configuración SSE (experimental).

## Usando `ssh` como Puente

La forma más segura de conectar un servidor remoto es tuneleando `stdio` a través de SSH.

```json
{
  "mcpServers": {
    "servidor-remoto-aws": {
      "command": "ssh",
      "args": [
        "-i",
        "/path/to/key.pem",
        "user@ec2-ip-address",
        "python /home/user/server/main.py"
      ]
    }
  }
}
```

Para Claude, esto es transparente: escribe en su `stdout` local, SSH lo lleva al servidor remoto, el servidor remoto responde en su `stdout`, y SSH lo trae de vuelta.

¡Voilá! Tienes acceso a herramientas en la nube desde tu escritorio local.
