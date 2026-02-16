# Subtema 5.3.1: elicitation/create: Formularios Dinámicos del Servidor

A veces una herramienta necesita un dato que el LLM no tiene y no puede adivinar.
Ejemplo: "Despliega esta app".
Pregunta obvia: "¿A qué entorno? ¿Staging o Prod?".

El servidor podría fallar con un error: "Falta el entorno".
Pero con **Elicitation**, el servidor puede pausar y preguntar al usuario.

## Request `elicitation/create`

El servidor envía al Host una petición para mostrar un formulario.

```json
{
  "method": "elicitation/create",
  "params": {
    "message": "Necesito saber el entorno de despliegue.",
    "fields": [
      {
        "name": "env",
        "type": "string",
        "description": "El entorno destino",
        "enum": ["staging", "production"], // Opciones cerradas
        "required": true
      }
    ]
  }
}
```

## Interacción UI

El Host (Claude Desktop) renderizará nativamente un diálogo modal o un formulario en el chat con un dropdown "staging / production".

## Response

Cuando el usuario rellena y envía, el servidor recibe:

```json
{
  "result": {
    "env": "production"
  }
}
```

Y ahora el servidor puede continuar su lógica.
