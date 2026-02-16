# Subtema 9.3.3: Auditoría de Seguridad: Checklist

Antes de desplegar tu servidor MCP en producción, verifica estos puntos:

## Transporte y Red

- [ ] ¿Uso HTTPS/WSS para conexiones remotas?
- [ ] ¿El endpoint `/sse` requiere autenticación?
- [ ] ¿Estoy validando el header `Host` para prevenir DNS Rebinding?

## Datos e Inputs

- [ ] ¿Tengo esquemas estrictos para todos los argumentos de herramientas?
- [ ] ¿Sanitizo las rutas de archivos para evitar Path Traversal?
- [ ] ¿Evito poner secretos (API keys) en logs o mensajes de error?

## Ejecución

- [ ] ¿Las herramientas destructivas piden confirmación explícita?
- [ ] ¿El servidor corre con un usuario del sistema operativo limitado (no root)?
- [ ] ¿Tengo timeouts configurados para evitar herramientas colgadas?

## Privacidad

- [ ] ¿Mis `Resources` exponen solo lo necesario y no todo el disco?
- [ ] ¿Están protegidos los logs contra inyección de caracteres de control?
