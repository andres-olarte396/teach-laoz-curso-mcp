# Subtema 5.5.2: Implementando un Sistema de Archivos Virtual (Read-Only)

Vamos a crear un servidor que expone una "memoria interna" (un diccionario de Python) como si fuera un sistema de archivos navegable.

## Escenario

Tenemos datos en memoria:

```python
DATA = {
    "notas": {
        "reunion.txt": "Acordamos usar MCP.",
        "compras.txt": "Leche, Pan, GPU."
    },
    "config": {
        "server.json": '{"port": 8080}'
    }
}
```

Queremos que el LLM pueda listar `mem://notas/` y leer `mem://notas/reunion.txt`.

## Implementación (Python + FastMCP)

```python
from fastmcp import FastMCP

mcp = FastMCP("VirtualFS")

# Datos en memoria (nuestro "disco")
VIRTUAL_FS = {
    "notas": ["reunion.txt", "compras.txt"],
    "config": ["server.json"]
}

FILE_CONTENTS = {
    "notas/reunion.txt": "Acordamos usar MCP.",
    "notas/compras.txt": "Leche, Pan, GPU.",
    "config/server.json": '{"port": 8080}'
}

@mcp.resource("mem://list")
def list_root() -> str:
    """Lista las carpetas en la raíz."""
    return "\n".join(VIRTUAL_FS.keys())

@mcp.resource("mem://{folder}/list")
def list_folder(folder: str) -> str:
    """Lista los archivos en una carpeta virtual."""
    if folder not in VIRTUAL_FS:
        raise ValueError("Carpeta no existe")
    return "\n".join(VIRTUAL_FS[folder])

@mcp.resource("mem://{folder}/{filename}")
def read_file(folder: str, filename: str) -> str:
    """Lee el contenido de un archivo virtual."""
    path = f"{folder}/{filename}"
    if path not in FILE_CONTENTS:
        raise ValueError("Archivo no existe")
    return FILE_CONTENTS[path]

if __name__ == "__main__":
    mcp.run()
```

## Pruebas con Claude

1.  **Usuario:** "¿Qué carpetas hay en memoria?"
2.  **Claude:** Usa `mem://list`. Respuesta: "notas\nconfig".
3.  **Usuario:** "¿Qué hay en notas?"
4.  **Claude:** Usa `mem://notas/list`. Respuesta: "reunion.txt\ncompras.txt".
5.  **Usuario:** "Lee la nota de la reunión."
6.  **Claude:** Usa `mem://notas/reunion.txt`. Respuesta: "Acordamos usar MCP."

¡Magia! Hemos creado una interfaz de exploración de archivos sobre datos puramente en memoria.
