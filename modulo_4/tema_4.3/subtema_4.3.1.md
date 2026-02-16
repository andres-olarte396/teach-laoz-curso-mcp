# Subtema 4.3.1: Autocompletado en Tiempo Real (Completion)

Cuando un usuario interactúa con un prompt o argumento en el Host, MCP permite ofrecer sugerencias de autocompletado en tiempo real.

## Uso Común

- Sugerir nombres de tablas de base de datos.
- Sugerir nombres de ramas de Git.
- Sugerir rutas de archivos.

## Request `completion/complete`

El host envía lo que el usuario ha escrito hasta el momento (`argument.value`) y el nombre de la referencia (Prompt o Resource Template).

```json
{
  "method": "completion/complete",
  "params": {
    "ref": { "type": "ref/prompt", "name": "analyze-table" },
    "argument": {
      "name": "table_name",
      "value": "user_"
    }
  }
}
```

## Response

El servidor busca coincidencias y responde con una lista de valores posibles.

```json
{
  "result": {
    "completion": {
      "values": ["user_profiles", "user_sessions", "user_logs"],
      "total": 3,
      "hasMore": false
    }
  }
}
```

El Host mostrará un desplegable al usuario:

- `user_profiles`
- `user_sessions`
- `user_logs`
