# Subtema 1.2.2: Negociación de Capacidades (Capability Negotiation)

El protocolo MCP es muy flexible. No todos los servidores soportan todas las características (algunos solo tienen Resources, otros solo Tools). Para manejar esto, existe una fase inicial de **negociación**.

## El Handshake (Apretón de Manos)

Al conectar, el primer mensaje que envía el cliente es **`initialize`**.

### Solicitud del Cliente (`initialize`)

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "initialize",
  "params": {
    "protocolVersion": "2024-11-05",
    "capabilities": {
      "roots": { "listChanged": true },
      "sampling": {}
    },
    "clientInfo": {
      "name": "Claude Desktop",
      "version": "1.0.0"
    }
  }
}
```

- **protocolVersion:** La versión del protocolo que el cliente quiere usar.
- **capabilities:** Qué características soporta el cliente (ej: ¿puede manejar cambios en raíces de archivos? ¿soporta sampling?).
- **clientInfo:** Nombre y versión del cliente para logs/debugging.

### Respuesta del Servidor

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "protocolVersion": "2024-11-05",
    "capabilities": {
      "logging": {},
      "prompts": { "listChanged": true },
      "resources": { "subscribe": true },
      "tools": { "listChanged": true }
    },
    "serverInfo": {
      "name": "My Postgres Server",
      "version": "0.1.0"
    }
  }
}
```

- **protocolVersion:** La versión que el servidor ha aceptado usar.
- **capabilities:** Qué características ofrece el servidor. En este ejemplo, soporta logging, prompts, resources (con suscripciones) y tools.
- **serverInfo:** Identidad del servidor.

## Notificación `notifications/initialized`

Una vez que el cliente recibe la respuesta de inicialización y está satisfecho, **debe** enviar una notificación final para confirmar que la conexión está lista.

```json
{
  "jsonrpc": "2.0",
  "method": "notifications/initialized"
}
```

Hasta que se reciba esta notificación, el servidor no debe enviar ninguna otra solicitud o notificación al cliente.
