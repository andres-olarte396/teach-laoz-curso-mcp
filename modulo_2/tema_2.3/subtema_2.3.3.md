# Subtema 2.3.3: Resumability y Reconexión con Last-Event-ID

La reconexión no es suficiente si se pierden mensajes durante el corte.

Imagine este escenario:

1.  El Servidor envía el mensaje con ID 100.
2.  La conexión se corta.
3.  El Servidor intenta enviar el mensaje 101, pero falla.
4.  El Cliente reconecta.

¿Cómo sabe el servidor que debe re-enviar el mensaje 101?

## Header `Last-Event-ID`

El cliente debe llevar la cuenta del último ID de mensaje que procesó correctamente.

Al reconectar, envía:

```http
POST /mcp HTTP/1.1
X-Mcp-Session-Id: session-123
Last-Event-ID: 100
```

El servidor ve esto y dice: "Ah, el cliente se quedó en el 100. Tengo en mi buffer los mensajes 101, 102 y 103. Se los envío ahora mismo".

Esto garantiza **entrega ordenada y sin pérdidas** (at-least-once o exactly-once dependiendo de la implementación), crucial para la fiabilidad de los agentes de IA.
