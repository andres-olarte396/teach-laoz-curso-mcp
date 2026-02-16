# Subtema 4.3.2: Proyecto Práctico: Servidor MCP de Documentación Técnica

Vamos a construir un servidor que sirva archivos Markdown locales como recursos, añada un prompt para resumirlos y soporte autocompletado de nombres de archivo.

## Código Base (Python + FastMCP)

```python
from fastmcp import FastMCP
import glob
import os

mcp = FastMCP("DocsServer")
DOCS_DIR = "./docs" # Asegúrate de crear este directorio y poner algunos .md

# 1. Recurso: Listar Documentos
@mcp.resource("docs://list")
def list_docs() -> str:
    """Lista todos los archivos de documentación disponibles."""
    files = glob.glob(os.path.join(DOCS_DIR, "*.md"))
    return "\n".join([os.path.basename(f) for f in files])

# 2. Recurso Template: Leer Documento Específico
@mcp.resource("docs://read/{filename}")
def read_doc(filename: str) -> str:
    """Lee el contenido de un archivo markdown específico."""
    path = os.path.join(DOCS_DIR, filename)
    if not os.path.exists(path):
        raise ValueError(f"Documento {filename} no encontrado")

    with open(path, "r", encoding="utf-8") as f:
        return f.read()

# 3. Prompt: Resumir Documento
@mcp.prompt()
def summarize_doc(filename: str) -> str:
    """Crea un prompt para pedir al LLM que resuma un documento."""
    content = read_doc(filename)
    return [
        {
            "role": "user",
            "content": f"Por favor resume el siguiente documento técnico:\n\n---\n{content}\n---"
        }
    ]

# 4. Autocompletado para el argumento 'filename'
# Nota: FastMCP simplifica esto, pero conceptualmente responde a completion/complete
# (En FastMCP actual, el soporte de autocompletado puede requerir decoradores adicionales o lógica manual dependiendo de la versión)

if __name__ == "__main__":
    mcp.run()
```

## Ejercicio para el Estudiante

1.  Crea una carpeta `docs` y pon archivos `api.md`, `architecture.md`.
2.  Ejecuta el servidor y conecta Claude Desktop.
3.  Usa el Prompt "Summarize Doc" y observa cómo te pide el argumento `filename`.
4.  Intenta implementar la lógica de `completion/complete` manualmente si usas el SDK raw.
