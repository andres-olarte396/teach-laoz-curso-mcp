# Subtema 5.2.2: Listado y Notificaciones: roots/list y roots/list_changed

Al igual que `tools/list`, el servidor puede preguntar al cliente qué raíces hay.

## Request `roots/list`

El servidor envía:

```json
{
  "method": "roots/list"
}
```

## Response

El cliente responde con la lista de directorios activos:

```json
{
  "result": {
    "roots": [
      {
        "uri": "file:///Users/andres/proyectos/mi-web",
        "name": "mi-web"
      },
      {
        "uri": "file:///Users/andres/proyectos/backend-api",
        "name": "backend-api"
      }
    ]
  }
}
```

## Notificación de Cambio (`notifications/roots/list_changed`)

Si el usuario abre una nueva carpeta en su editor o cierra una existente, el Host envía esta notificación al servidor.

El servidor, al recibirla, debería volver a pedir `roots/list` y actualizar su contexto interno (ej: re-indexar archivos, limpiar cachés de archivos cerrados).

### Implementación en Servidor

Es buena práctica suscribirse a este evento al inicio.

```python
# Pseudo-código
server.on("notifications/roots/list_changed", async () => {
    roots = await server.list_roots();
    indexer.update_scope(roots);
});
```
