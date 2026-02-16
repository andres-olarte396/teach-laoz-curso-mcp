# Subtema 2.3.2: Gestión de Sesiones: Mcp-Session-Id y Estado del Servidor

Aunque Streamable HTTP intenta mantener una conexión persistente, en el mundo real las conexiones se cortan (timeout, cambio de red, reinicio de servidor).

Para manejar esto, MCP introduce el concepto de **Sesión**.

## Header `X-Mcp-Session-Id`

Cada vez que un cliente se conecta, debe enviar o recibir un ID de sesión.

1.  **Cliente conecta por primera vez:** No envía ID.
2.  **Servidor crea sesión:** Genera un UUID (ej: `session-123`) y lo devuelve en el header de respuesta `X-Mcp-Session-Id`.
3.  **Cliente reconecta:** Si la conexión se cae, el cliente intenta reconectar enviando `X-Mcp-Session-Id: session-123` en su petición.

## Estado del Servidor

El servidor debe mantener el estado de esa sesión (herramientas negociadas, recursos suscritos) en memoria (o en una base de datos distribuida como Redis para escalabilidad real).

Si el servidor recibe un ID de sesión que no conoce (porque se reinició y perdió la memoria), debe responder con un error `400 Bad Request` o `410 Gone`, obligando al cliente a reiniciar el handshake `initialize`.
