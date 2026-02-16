# Subtema 3.2.3: Notificaciones de Cambio: tools/list_changed

Las herramientas no son estáticas. Un servidor podría dinámicamente añadir nuevas funciones basándose en el contexto (ej: conexión a una base de datos exitosa).

## El Problema de la Caché

Los clientes MCP (Hosts) suelen cachear la lista de herramientas al inicio (`initialize`) para no preguntar en cada turno de conversación. Si añades una herramienta después, el Host no la verá.

## La Solución: Notificación

Si la lista de herramientas cambia, el servidor debe enviar una notificación proactiva:

```json
{
  "jsonrpc": "2.0",
  "method": "notifications/tools/list_changed"
}
```

## Reacción del Cliente

Al recibir esto, el cliente sabe que su caché está sucia e inmediatamente enviará una nueva petición `tools/list` para obtener la versión actualizada.

### Ejemplo de Uso

Imagina un servidor de plugins.

1.  Inicio: Solo tiene herramienta `install_plugin`.
2.  Usuario: "Instala el plugin de clima".
3.  Servidor: Instala plugin, carga herramienta `get_weather`.
4.  Servidor: Envía `notifications/tools/list_changed`.
5.  Cliente: Refresca lista. Ahora ve `get_weather`.
6.  Usuario: "Dime el clima". (Ahora es posible).
