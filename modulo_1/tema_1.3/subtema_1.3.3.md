# Subtema 1.3.3: Manejo de Errores: Códigos Estándar y Personalizados

Cuando algo falla en MCP, debemos ser precisos. Un simple "Error" no ayuda al LLM a corregirse.

## Códigos de Error JSON-RPC Estándar

Estos son universales y debes usarlos cuando aplique:

| Código     | Significado      | Cuándo usarlo                                                                       |
| :--------- | :--------------- | :---------------------------------------------------------------------------------- |
| **-32700** | Parse Error      | El JSON recibido está mal formado.                                                  |
| **-32600** | Invalid Request  | El JSON es válido pero no es una Request válida (falta `method`, etc.).             |
| **-32601** | Method Not Found | El cliente pidió un método (`generar_imagen`) que no existe.                        |
| **-32602** | Invalid Params   | Los argumentos pasados a la herramienta son incorrectos (ej: string en vez de int). |
| **-32603** | Internal Error   | Excepción no manejada en tu servidor.                                               |

## Errores de Aplicación

Para errores específicos de tu lógica (ej: "Base de datos no disponible", "Archivo no encontrado"), puedes usar códigos fuera del rango reservado (-32000 a -32768).

## Ejemplo Práctico: Implementando `Method Not Found`

```python
def procesar_mensaje(mensaje_json):
    metodo = mensaje_json.get("method")

    if metodo == "tools/list":
        return listar_herramientas()

    elif metodo == "tools/call":
        return ejecutar_herramienta(mensaje_json["params"])

    else:
        # Método desconocido: Devolvemos error estándar -32601
        return {
            "jsonrpc": "2.0",
            "error": {
                "code": -32601,
                "message": f"Method '{metodo}' not found"
            },
            "id": mensaje_json.get("id")
        }
```
