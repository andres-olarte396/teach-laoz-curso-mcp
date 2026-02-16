# Subtema 5.4.2: Reporte de Progreso: notifications/progress

Ya mencionamos el progreso en herramientas de larga duración, pero aquí profundizamos en el mecanismo.

## Tokens de Progreso

El progreso siempre está vinculado a una solicitud específica (usualmente `tools/call` o `resources/read`).

El cliente genera un `progressToken` (puede ser un número o string) y lo envía en la petición original.

```json
// Cliente pide herramienta
{
  "method": "tools/call",
  "params": {
    "name": "backup_db",
    "_meta": { "progressToken": 101 } // La ubicación exacta depende de la versión del spec
  }
}
```

## Notificación del Servidor

El servidor emite notificaciones usando ese token.

```json
{
  "method": "notifications/progress",
  "params": {
    "progressToken": 101,
    "progress": 45, // Valor actual
    "total": 100 // Valor máximo (opcional)
  }
}
```

## UX en el Host

- Si `total` está presente: Barra de progreso determinista (45%).
- Si `total` falta: Spinner o barra indeterminada ("Cargando...").

Es vital usar esto para operaciones > 2 segundos, o el usuario pensará que la IA se ha congelado.
