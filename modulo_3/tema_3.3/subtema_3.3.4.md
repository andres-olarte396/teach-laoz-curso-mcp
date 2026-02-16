# Subtema 3.3.4: Proyecto Práctico: Servidor MCP de Gestión de Base de Datos

Vamos a poner todo junto creando un servidor real.

## Objetivo

Construir un servidor MCP que permita a Claude interactuar con una base de datos SQLite local para gestionar una lista de tareas (To-Do List).

## Requisitos

El servidor debe exponer herramientas para:

1.  `create_table`: Inicializar la tabla `todos` si no existe.
2.  `add_todo`: Añadir una tarea.
3.  `list_todos`: Listar tareas (con filtro opcional por estado).
4.  `complete_todo`: Marcar una tarea como completada.

## Código Base (Python + FastMCP)

Usaremos la librería `fastmcp` por su simplicidad.

```python
from fastmcp import FastMCP
import sqlite3

mcp = FastMCP("TodoManager")
DB_FILE = "todos.db"

def get_db():
    conn = sqlite3.connect(DB_FILE)
    conn.row_factory = sqlite3.Row
    return conn

@mcp.tool()
def init_db() -> str:
    """Crea la tabla de tareas si no existe."""
    with get_db() as conn:
        conn.execute("""
            CREATE TABLE IF NOT EXISTS todos (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                title TEXT NOT NULL,
                status TEXT DEFAULT 'pending'
            )
        """)
    return "Base de datos inicializada correctamente."

@mcp.tool()
def add_todo(title: str) -> str:
    """Añade una nueva tarea."""
    with get_db() as conn:
        cursor = conn.execute("INSERT INTO todos (title) VALUES (?)", (title,))
        id_tarea = cursor.lastrowid
    return f"Tarea creada con ID {id_tarea}"

@mcp.tool()
def list_todos(status: str = None) -> str:
    """Lista las tareas, opcionalmente filtrando por estado ('pending' o 'completed')."""
    with get_db() as conn:
        if status:
            rows = conn.execute("SELECT * FROM todos WHERE status = ?", (status,)).fetchall()
        else:
            rows = conn.execute("SELECT * FROM todos").fetchall()

    tasks = [dict(row) for row in rows]
    return str(tasks)

@mcp.tool()
def complete_todo(id: int) -> str:
    """Marca una tarea como completada."""
    with get_db() as conn:
        cursor = conn.execute("UPDATE todos SET status = 'completed' WHERE id = ?", (id,))
        if cursor.rowcount == 0:
            return f"Error: No se encontró tarea con ID {id}"
    return f"Tarea {id} completada."

if __name__ == "__main__":
    mcp.run()
```

## Instrucciones de Uso

1.  Instala dependencias: `pip install fastmcp`
2.  Guarda como `server.py`
3.  Configura Claude Desktop para ejecutar este script.
4.  Dile a Claude: "Crea una base de datos de tareas, añade 'Comprar leche' y luego lístalas".
