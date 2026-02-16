# Subtema 4.2.1: Definición de Prompts: name, description y arguments

## ¿Qué es un Prompt en MCP?

Un **Prompt** en MCP no es lo que escribes en el chat ("Hola, ¿cómo estás?").
Es una **plantilla reutilizable** que el servidor ofrece al usuario para iniciar una interacción específica.

Ejemplos:

- "Analizar Logs de Error"
- "Escribir Test Unitario para esta función"
- "Resumir Hilo de Slack"

## Estructura

Similar a una Tool, un Prompt tiene metadatos:

```json
{
  "name": "analyze-error",
  "description": "Analiza un stacktrace y sugiere soluciones",
  "arguments": [
    {
      "name": "error_log",
      "description": "El texto del error",
      "required": true
    }
  ]
}
```

El Host usa esto para mostrar un menú o interfaz gráfica donde el usuario puede seleccionar "Analyze Error" y rellenar el campo "Error Log".
