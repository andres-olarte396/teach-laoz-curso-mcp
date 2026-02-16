# Subtema 3.1.3: Invocación: El Flujo tools/call y Tipos de Contenido de Respuesta

Cuando el modelo decide usar una herramienta, el Host envía el comando de ejecución.

## Request `tools/call`

```json
{
  "jsonrpc": "2.0",
  "method": "tools/call",
  "id": 2,
  "params": {
    "name": "get_weather",
    "arguments": {
      "city": "Madrid",
      "days": 1
    }
  }
}
```

## Response

La respuesta de una herramienta es una lista de "contenidos". Puede devolver texto, imágenes o recursos binarios.

```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "result": {
    "content": [
      {
        "type": "text",
        "text": "El clima en Madrid es Soleado, 25°C."
      }
    ],
    "isError": false
  }
}
```

### Manejo de Errores (`isError`)

Si la herramienta falla (ej: ciudad no encontrada), NO debes devolver un error JSON-RPC (a menos que sea un fallo del protocolo).
Debes devolver una respuesta válida con el error en el texto y el flag `isError: true`.

```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "result": {
    "content": [
      {
        "type": "text",
        "text": "Error: La ciudad 'Atlantis' no existe en la base de datos."
      }
    ],
    "isError": true
  }
}
```

De esta forma, el LLM **lee el error** y puede intentar corregirse (ej: "¿Quizás quisiste decir 'Atlanta'?"). Si devolvieras una excepción de protocolo, la conversación podría romperse.
