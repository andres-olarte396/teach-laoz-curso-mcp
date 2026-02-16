# Subtema 0.1.1: JSON como Formato de Intercambio de Datos

## ¿Qué es JSON?

**JSON (JavaScript Object Notation)** es un formato ligero para el intercambio de datos. Es fácil de leer y escribir para los humanos, y fácil de analizar y generar para las máquinas. Es el estándar de facto para la comunicación entre clientes y servidores modernos, y es la base fundamental del protocolo MCP.

## Sintaxis Básica

JSON se basa en dos estructuras:

1. **Colección de pares clave/valor** (como un objeto en JavaScript, diccionario en Python, o mapa en Java).
2. **Lista ordenada de valores** (como un array, vector o lista).

### Ejemplo de Objeto JSON

```json
{
  "nombre": "Servidor MCP Demo",
  "version": 1,
  "activo": true,
  "tags": ["mcp", "demo", "json-rpc"],
  "config": {
    "puerto": 3000,
    "host": "localhost"
  },
  "null_value": null
}
```

## Tipos de Datos en JSON

- **String (Cadena):** Texto entre comillas dobles. `"Hola Mundo"`.
- **Number (Número):** Enteros o flotantes. `42`, `3.14`.
- **Boolean (Booleano):** `true` o `false`.
- **Array (Arreglo):** Lista ordenada entre corchetes `[]`. `[1, 2, 3]`.
- **Object (Objeto):** Colección desordenada de pares clave/valor entre llaves `{}`.
- **Null:** Valor nulo. `null`.

## JSON vs XML

Aunque XML fue popular en el pasado, JSON lo ha desplazado en la mayoría de las APIs modernas debido a su simplicidad y menor peso.

| Característica  | JSON                            | XML                               |
| :-------------- | :------------------------------ | :-------------------------------- |
| **Legibilidad** | Alta, sintaxis limpia           | Media, verboso con etiquetas      |
| **Tamaño**      | Ligero                          | Pesado (etiquetas de cierre)      |
| **Parsing**     | Nativo en JS, rápido            | Complejo, requiere parser DOM/SAX |
| **Esquema**     | Flexible (opcional JSON Schema) | Rígido (XSD, DTD)                 |

## ¿Por qué es crucial para MCP?

El protocolo **MCP utiliza JSON-RPC 2.0** como su mecanismo de mensajería. Cada solicitud, respuesta o notificación que viaja entre el host y el servidor MCP es un mensaje JSON.

Entender la estructura de JSON es el primer paso para poder depurar y construir herramientas MCP.

## Ejemplos Prácticos de Manejo de JSON

Una habilidad esencial para MCP es poder leer (parsear) y escribir (generar) JSON desde tu lenguaje de programación.

### En JavaScript / TypeScript

JavaScript tiene soporte nativo para JSON a través del objeto global `JSON`.

```javascript
// 1. JSON.stringify: Convertir Objeto -> String JSON
const herramienta = {
  name: "get_weather",
  description: "Obtiene el clima actual",
  inputSchema: {
    type: "object",
    properties: {
      city: { type: "string" },
    },
  },
};

const jsonString = JSON.stringify(herramienta, null, 2); // 'null, 2' para indentación bonita
console.log(jsonString);
// Salida:
// {
//   "name": "get_weather",
//   "description": "Obtiene el clima actual",
//   ...
// }

// 2. JSON.parse: Convertir String JSON -> Objeto
const respuestaServidor = '{"jsonrpc": "2.0", "result": "ok", "id": 1}';

try {
  const objeto = JSON.parse(respuestaServidor);
  console.log(objeto.result); // "ok"
} catch (error) {
  console.error("Error: JSON inválido");
}
```

### En Python

Python utiliza el módulo estándar `json`.

```python
import json

# 1. json.dumps: Convertir Diccionario -> String JSON
herramienta = {
    "name": "get_weather",
    "description": "Obtiene el clima actual",
    "inputSchema": {
        "type": "object",
        "properties": {
            "city": {"type": "string"}
        }
    }
}

# indent=2 hace que sea legible
json_string = json.dumps(herramienta, indent=2)
print(json_string)

# 2. json.loads: Convertir String JSON -> Diccionario
respuesta_servidor = '{"jsonrpc": "2.0", "result": "ok", "id": 1}'

try:
    data = json.loads(respuesta_servidor)
    print(data["result"]) # "ok"
except json.JSONDecodeError:
    print("Error: JSON inválido")
```
