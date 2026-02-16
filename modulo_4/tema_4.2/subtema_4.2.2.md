# Subtema 4.2.2: Resolución de Prompts: prompts/get y Mensajes Multi-Rol

Cuando el usuario selecciona un Prompt y rellena los argumentos, el Host pide al servidor que "resuelva" (renderice) el prompt.

## Request `prompts/get`

```json
{
  "method": "prompts/get",
  "params": {
    "name": "analyze-error",
    "arguments": {
      "error_log": "TypeError: cannot read property 'foo' of undefined..."
    }
  }
}
```

## Response

El servidor devuelve una lista de mensajes que se insertarán en la conversación como si el usuario o el asistente los hubieran escrito.

```json
{
  "result": {
    "messages": [
      {
        "role": "user",
        "content": {
          "type": "text",
          "text": "Aquí tienes el error: TypeError..."
        }
      },
      {
        "role": "assistant", // Opcional (pre-fill)
        "content": {
          "type": "text",
          "text": "Veo que es un error de tipo. Analicemos..."
        }
      }
    ]
  }
}
```

Esto permite al servidor **controlar el contexto inicial** de la conversación, asegurando que el LLM tenga toda la información necesaria formateada correctamente.
