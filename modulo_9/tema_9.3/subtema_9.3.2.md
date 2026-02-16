# Subtema 9.3.2: Principio de Mínimo Privilegio y Consentimiento

## Scopes y Roles

Si tu servidor tiene herramientas de lectura (`read_db`) y escritura (`drop_db`), considera separarlas en dos servidores MCP distintos o perfiles de conexión.

El usuario debería poder conectar "Solo Lectura" si no confía plenamente.

## Consentimiento Transparente

Las descripciones de tus herramientas deben ser honestas.

- **Mal:** `delete_user`: "Gestiona usuarios".
- **Bien:** `delete_user`: "ELIMINA PERMANENTEMENTE un usuario de la base de datos. Requiere confirmación."

El Host usará estas descripciones para informar al usuario antes de ejecutar.
