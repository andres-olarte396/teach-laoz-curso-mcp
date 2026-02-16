# Subtema 3.1.2: Descubrimiento: El Flujo tools/list y Paginación

Para que un Host sepa qué herramientas tienes, debe preguntar.

## Request `tools/list`

El cliente envía:

```json
{
  "jsonrpc": "2.0",
  "method": "tools/list",
  "id": 1,
  "params": {
    "cursor": "abc-123" // Opcional, para paginación
  }
}
```

## Response

El servidor responde con la lista de herramientas:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "tools": [
      { "name": "tool_a", ... },
      { "name": "tool_b", ... }
    ],
    "nextCursor": "def-456" // Si hay más páginas
  }
}
```

### Paginación

Si tu servidor tiene miles de herramientas (ej: un servidor que expone 5000 funciones de una librería de Python), no puedes enviarlas todas en un solo mensaje JSON-RPC.

El protocolo soporta **Paginación Basada en Cursores**.

1.  Servidor devuelve las primeras 100 herramientas y un `nextCursor`.
2.  Cliente ve `nextCursor` y hace otra petición `tools/list` pasando ese cursor en `params`.
3.  Se repite hasta que el servidor devuelva `nextCursor: null`.

> **Nota:** La mayoría de los servidores simples devolverán todas las herramientas de una vez y `nextCursor: null`.
