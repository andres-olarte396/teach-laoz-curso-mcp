# Subtema 4.1.2: Listado y Lectura: resources/list y resources/read

Para que el modelo pueda usar tus recursos, primero debe saber que existen.

## 1. Listar Recursos (`resources/list`)

El cliente pide la lista ("catálogo") de recursos disponibles.

```json
// Request
{
  "method": "resources/list"
}

// Response
{
  "result": {
    "resources": [
      {
        "uri": "memo://note/welcome",
        "name": "Nota de Bienvenida",
        "description": "Instrucciones básicas para el usuario",
        "mimeType": "text/markdown"
      }
    ]
  }
}
```

Es importante dar un `name` y `description` claros, ya que el LLM los usará para decidir si necesita leer ese recurso.

## 2. Leer un Recurso (`resources/read`)

Cuando el LLM decide que necesita el contenido, el Host envía:

```json
// Request
{
  "method": "resources/read",
  "params": {
    "uri": "memo://note/welcome"
  }
}

// Response
{
  "result": {
    "contents": [
      {
        "uri": "memo://note/welcome",
        "mimeType": "text/markdown",
        "text": "# Bienvenido a mi servidor MCP..."
      }
    ]
  }
}
```

### Nota sobre "Contents"

La respuesta es una lista `contents` porque una sola URI podría (teóricamente) resolver a múltiples fragmentos, aunque lo normal es uno.
