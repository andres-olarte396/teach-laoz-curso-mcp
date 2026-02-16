# Subtema 3.1.1: Definición de Herramientas: Name, Description e inputSchema

## ¿Qué es una Tool?

Una **Tool** es la primitiva más potente de MCP. Permite al modelo realizar acciones en el mundo exterior (leer archivos, ejecutar SQL, llamar a una API) o realizar cálculos complejos.

Desde la perspectiva del protocolo, una Tool es una definición JSON que el servidor envía al cliente.

## Estructura JSON de una Tool

```json
{
  "name": "get_weather",
  "description": "Obtiene el pronóstico del tiempo actual para una ciudad.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "city": {
        "type": "string",
        "description": "El nombre de la ciudad (ej: Madrid, Tokyo)"
      },
      "days": {
        "type": "integer",
        "description": "Número de días (1-5)",
        "default": 1
      }
    },
    "required": ["city"]
  }
}
```

### Componentes Clave

1.  **name:** Identificador único. Debe ser claro y conciso (usualmente `snake_case`).
2.  **description:** **CRÍTICO.** Es lo que lee el LLM para saber cuándo usar esta herramienta. Una buena descripción mejora drásticamente la precisión del modelo.
3.  **inputSchema:** Define los argumentos que la herramienta acepta usando el estándar **JSON Schema Draft 7**. El modelo usará este esquema para generar el JSON de la llamada.

## JSON Schema

Es vital que domines JSON Schema.

- `type`: string, number, integer, boolean, object, array.
- `enum`: Para limitar opciones (ej: `["celsius", "fahrenheit"]`).
- `description` (en propiedades): Ayuda al modelo a entender qué valor poner en cada campo.

## Ejemplo en Python (SDK)

```python
@mcp.tool()
def get_weather(city: str, days: int = 1) -> str:
    """Obtiene el clima.

    Args:
        city: Ciudad a consultar.
        days: Días de pronóstico.
    """
    return f"Clima en {city} por {days} días..."
```

El SDK de Python usa los _type hints_ y el _docstring_ para generar el JSON Schema automáticamente.
