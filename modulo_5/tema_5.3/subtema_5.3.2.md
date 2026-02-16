# Subtema 5.3.2: Casos de Uso: Confirmación, Credenciales y Desambiguación

## 1. Confirmación de Acciones Destructivas

Aunque usemos `destructive` hints, a veces queremos una confirmación explícita con lógica de negocio custom.

```json
{
  "method": "elicitation/create",
  "params": {
    "message": "Vas a borrar la base de datos de PRODUCCIÓN. Escribe el nombre de la DB para confirmar.",
    "fields": [{ "name": "confirmation", "required": true }]
  }
}
```

## 2. Recolección de Credenciales (On-the-fly)

Si tu servidor conecta a un servicio externo (ej: GitHub) y no tiene token, puede pedirlo en tiempo de ejecución en lugar de fallar al inicio.

> **Nota:** El Host debe manejar estos campos de forma segura (tipo `password`), aunque hoy día el soporte de campos ocultos en MCP varía por cliente.

## 3. Desambiguación

Usuario: "Reinicia el servidor".
Servidor: (Ve que hay 3 servidores corriendo).

En lugar de que el LLM tenga que adivinar o preguntar en chat (que es lento y gasta tokens), el servidor lanza un Elicitation:
"Hay 3 servidores. ¿Cuál reinicio?"
[ ] WebServer
[ ] Worker
[ ] Database

El usuario hace clic y listo. Cero alucinaciones.
