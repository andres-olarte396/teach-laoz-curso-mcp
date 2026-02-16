# Subtema 4.1.4: Suscripciones: Notificación de Cambios en Recursos

Los recursos no siempre son estáticos. Un log crece, un archivo se edita. MCP permite que el Host se "suscriba" a un recurso para recibir actualizaciones en tiempo real.

## Flujo de Suscripción

1.  **Suscripción:** Cliente envía `resources/subscribe` con la URI.
2.  **Confirmación:** Servidor responde OK.

## Notificación de Cambio

Cuando el dato cambia en el servidor (ej: alguien escribió en el log), el servidor envía una notificación:

```json
{
  "method": "notifications/resources/updated",
  "params": {
    "uri": "file:///var/log/syslog"
  }
}
```

> **Importante:** La notificación NO contiene el nuevo contenido. Solo avisa "esto cambió".

## Reacción del Host

Al recibir la notificación, el Host decide si quiere leer el nuevo contenido (enviando `resources/read` de nuevo) o ignorarlo. Esto evita saturar la red enviando datos que quizás el usuario ya no está mirando.
