# Subtema 1.3.1: Anatomía de un Mensaje JSON-RPC: Request, Response, Notification

MCP se construye sobre **JSON-RPC 2.0**, un protocolo ligero de llamada a procedimientos remotos. Entenderlo es vital para depurar.

## Tipos de Mensajes

### 1. Request (Solicitud)

Un mensaje que espera una respuesta. DEBE tener un `id`.

```json
{
  "jsonrpc": "2.0",
  "method": "tools/call",
  "params": {
    "name": "get_weather",
    "arguments": { "city": "Madrid" }
  },
  "id": 1
}
```

### 2. Response (Respuesta Exitosa)

Responde a una solicitud específica usando el mismo `id`.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "content": [{ "type": "text", "text": "Soleado, 25C" }]
  },
  "id": 1
}
```

### 3. Error Response (Respuesta de Error)

Indica que algo salió mal.

```json
{
  "jsonrpc": "2.0",
  "error": {
    "code": -32601,
    "message": "Method not found"
  },
  "id": 1
}
```

### 4. Notification (Notificación)

Un mensaje que NO espera respuesta. NO tiene `id`. Ideal para logs o progresos.

```json
{
  "jsonrpc": "2.0",
  "method": "notifications/message",
  "params": {
    "level": "info",
    "data": "Servidor iniciado correctamente"
  }
}
```

## Ejercicio Práctico: Construcción Manual

Aunque los SDKs hacen esto por ti, intenta construir estos diccionarios en Python:

```python
import json

def crear_request(metodo, parametros, id_req):
    return {
        "jsonrpc": "2.0",
        "method": metodo,
        "params": parametros,
        "id": id_req
    }

req = crear_request("ping", {}, 123)
print(json.dumps(req, indent=2))
```
