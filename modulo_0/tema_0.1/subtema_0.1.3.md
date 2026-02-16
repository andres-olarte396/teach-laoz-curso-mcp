# Subtema 0.1.3: APIs REST: Diseño y Consumo

## ¿Qué es REST?

**REST (Representational State Transfer)** es un estilo arquitectónico para diseñar servicios web. Las APIs que siguen estos principios se llaman RESTful APIs. Utilizan HTTP y sus métodos (GET, POST, etc.) de manera semántica.

## Principios Clave

1.  **Stateless (Sin estado):** Cada petición debe contener toda la información necesaria. El servidor no guarda el estado de la sesión del cliente entre peticiones.
2.  **Recursos:** Todo es un recurso identificable por una URI (Uniform Resource Identifier). Ej: `/usuarios/123`.
3.  **Interfaz Uniforme:** Uso consistente de métodos HTTP y formatos de respuesta (usualmente JSON).

## Estructura de una API REST

Supongamos una API para gestionar **herramientas (tools)**:

- `GET /tools`: Obtener lista de todas las herramientas.
- `GET /tools/1`: Obtener detalles de la herramienta con ID 1.
- `POST /tools`: Crear una nueva herramienta. (Datos en el cuerpo del request).
- `PUT /tools/1`: Actualizar la herramienta 1.
- `DELETE /tools/1`: Eliminar la herramienta 1.

## Consumo de APIs

Como desarrollador de servidores MCP, a menudo tendrás que **consumir** APIs externas (ej: API de Weather, API de GitHub, API de Base de Datos) para exponer sus datos a través de MCP.

### Herramientas para probar APIs

- **curl:** Herramienta de línea de comandos.
- **Postman / Insomnia:** Clientes gráficos.
- **Extensiones de VS Code:** Thunder Client, REST Client.

## Relación con MCP

MCP **no es exactamente REST**, pero comparte conceptos.

- En lugar de múltiples endpoints REST, MCP usa **JSON-RPC** (generalmente sobre un solo canal).
- Sin embargo, al implementar **servidores MCP remotos**, utilizaremos conceptos de REST (especialmente en la negociación de conexión y en los endpoints SSE).
- Además, muchas **herramientas MCP** que crearás serán "envoltorios" (wrappers) sobre APIs REST existentes.

## Ejemplos Prácticos de Consumo de APIs

Vamos a consumir una API pública real: `https://jsonplaceholder.typicode.com/todos/1`

### 1. Usando `curl` (Línea de Comandos)

Es la forma más rápida de probar.

```bash
curl https://jsonplaceholder.typicode.com/todos/1
```

Para enviar datos (POST):

```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -d '{"title":"foo","body":"bar","userId":1}'
```

### 2. Usando Python (`requests`)

Es la librería estándar de facto en Python.

```python
import requests

# GET Request
response = requests.get('https://jsonplaceholder.typicode.com/todos/1')

if response.status_code == 200:
    data = response.json()
    print(f"Tarea: {data['title']}")
else:
    print(f"Error: {response.status_code}")

# POST Request
new_post = {"title": "foo", "body": "bar", "userId": 1}
response = requests.post('https://jsonplaceholder.typicode.com/posts', json=new_post)
print(response.json())
```

### 3. Usando Node.js / Browser (`fetch`)

API nativa moderna.

```javascript
// GET Request
fetch("https://jsonplaceholder.typicode.com/todos/1")
  .then((response) => response.json())
  .then((json) => console.log("Tarea:", json.title))
  .catch((err) => console.error("Error:", err));

// Async/Await (Más limpio)
async function crearPost() {
  const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    body: JSON.stringify({
      title: "foo",
      body: "bar",
      userId: 1,
    }),
    headers: {
      "Content-type": "application/json; charset=UTF-8",
    },
  });

  const json = await response.json();
  console.log(json);
}

crearPost();
```
