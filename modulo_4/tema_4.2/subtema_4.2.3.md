# Subtema 4.2.3: Prompts Dinámicos: Generación Contextual y Datos Embebidos

Lo poderoso de los Prompts MCP es que se generan **en el servidor**.

Esto significa que tu servidor puede consultar una base de datos, leer un archivo o llamar a una API externa _antes_ de devolver el texto del prompt.

## Ejemplo: "Resumir Ticket de Jira"

1.  Usuario selecciona prompt "Resumir Ticket" e introduce ID `PROJ-123`.
2.  Servidor recibe `prompts/get`.
3.  Servidor conecta a la API de Jira, descarga título, descripción y comentarios del ticket `PROJ-123`.
4.  Servidor construye un mensaje formateado con toda esa información.
5.  Servidor devuelve el mensaje al Host.

Para el LLM, es como si el usuario hubiera copiado y pegado manualmente todo el contenido del ticket, pero fue automático y sin errores.

## Embebiendo Recursos

Además de texto, un prompt puede devolver **recursos embebidos**.

```json
{
  "role": "user",
  "content": {
    "type": "resource",
    "resource": {
      "uri": "jira://issue/PROJ-123",
      "mimeType": "application/json",
      "text": "{...json data...}"
    }
  }
}
```

Esto es semanticamente más rico que el texto plano y ayuda al modelo a entender la estructura de los datos.
