# Subtema 3.3.2: Validación de Entrada y Sanitización para Seguridad

Nunca confíes en el LLM. Trátalo como a cualquier usuario externo: valida todo.

## Riesgos Comunes

1.  **Command Injection:** Si tu herramienta ejecuta comandos de shell con argumentos del LLM.
    - _Mal:_ `os.system(f"ping {host}")` -> El LLM podría enviar `8.8.8.8; rm -rf /`.
    - _Bien:_ Usa librerías que escapen argumentos o listas de argumentos (`subprocess.run(["ping", host])`).

2.  **Path Traversal:** Si tu herramienta lee archivos.
    - _Mal:_ `open(filename)` -> El LLM podría enviar `../../../../etc/passwd`.
    - _Bien:_ Valida que la ruta esté dentro de un directorio permitido.

## Validación con Pydantic (Python)

El SDK de Python se integra genial con Pydantic.

```python
from pydantic import BaseModel, Field, EmailStr

class CreateUserParams(BaseModel):
    name: str = Field(..., min_length=2, max_length=50)
    email: EmailStr
    age: int = Field(..., ge=18)

@mcp.tool()
def create_user(params: CreateUserParams):
    # Si llega aquí, params es seguro y válido.
    ...
```

Si el LLM envía un email inválido o una edad < 18, Pydantic lanzará un error que MCP convertirá automáticamente en una respuesta de error legible para el LLM, quien intentará corregirse solo.
