# Ejercicio Práctico Tema 0.1: Consumo y Parseo de Datos

## Objetivo

El objetivo de este ejercicio es consolidar tus conocimientos sobre **JSON y APIs REST**. Crearás un pequeño script (en Python o Node.js) que consuma una API pública, procese los datos JSON recibidos y muestre información específica en la consola.

Esta habilidad es **fundamental** para MCP, ya que muchas herramientas que crearás harán exactamente esto: consultar una fuente de datos externa y devolvérsela al LLM.

## Instrucciones

### Parte 1: Elegir tu Herramienta

Decide si usarás Python o Node.js para este ejercicio. Asegúrate de tener instalado el entorno según el Tema 0.3.

### Parte 2: Consumir la API de Usuarios

Usaremos la API pública de pruebas **JSONPlaceholder**.

1. **Endpoint:** `https://jsonplaceholder.typicode.com/users`
2. **Método:** `GET`
3. **Tarea:**
   - Realiza una petición HTTP GET a la URL.
   - Obtén la respuesta y asegúrate de que sea un JSON válido (una lista de usuarios).

### Parte 3: Procesar el JSON

La API devuelve una lista de objetos. Tu script debe recorrer esa lista y, para cada usuario, imprimir una línea con el siguiente formato:

```text
[ID] Nombre (Email) - Ciudad
```

**Ejemplo de salida esperada:**

```text
[1] Leanne Graham (Sincere@april.biz) - Gwenborough
[2] Ervin Howell (Shanna@melissa.tv) - Wisokyburgh
...
```

### Parte 4: Filtrado (Opcional - Reto)

Modifica tu script para que solo muestre los usuarios que viven en una ciudad que empiece con la letra "S" o "G".

## Solución Sugerida

Intenta resolverlo por tu cuenta antes de mirar el código.

### Solución en Python

```python
import requests

def obtener_usuarios():
    url = "https://jsonplaceholder.typicode.com/users"

    try:
        response = requests.get(url)
        response.raise_for_status() # Lanza error si status no es 200 OK

        usuarios = response.json()

        print("--- Lista de Usuarios ---")
        for usuario in usuarios:
            id_user = usuario['id']
            nombre = usuario['name']
            email = usuario['email']
            ciudad = usuario['address']['city']

            # Reto opcional: Filtrado
            # if ciudad.startswith(('S', 'G')):
            print(f"[{id_user}] {nombre} ({email}) - {ciudad}")

    except requests.exceptions.RequestException as e:
        print(f"Error al conectar con la API: {e}")

if __name__ == "__main__":
    obtener_usuarios()
```

### Solución en Node.js

```javascript
async function obtenerUsuarios() {
  const url = "https://jsonplaceholder.typicode.com/users";

  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const usuarios = await response.json();

    console.log("--- Lista de Usuarios ---");
    usuarios.forEach((usuario) => {
      const { id, name, email, address } = usuario;
      const ciudad = address.city;

      // Reto opcional: Filtrado
      // if (ciudad.startsWith('S') || ciudad.startsWith('G')) {
      console.log(`[${id}] ${name} (${email}) - ${ciudad}`);
      // }
    });
  } catch (error) {
    console.error("Error al conectar con la API:", error);
  }
}

obtenerUsuarios();
```

## Conclusión

¡Felicidades! Acabas de realizar la tarea fundamental de un servidor MCP: **fetch data -> process data**. En los próximos módulos, envolveremos esta lógica dentro de una **Tool MCP** para que sea Claude quien "ejecute" este código.
