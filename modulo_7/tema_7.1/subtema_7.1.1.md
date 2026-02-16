# Subtema 7.1.1: Instalación con uv y Configuración del Proyecto Python

El ecosistema de Python para MCP ha adoptado herramientas modernas. Recomendamos usar **uv** (el sucesor espiritual de pip/poetry escrito en Rust) para la gestión de dependencias, aunque `pip` estándar también funciona.

## Prerrequisitos

- Python 3.10+
- uv (opcional pero recomendado)

## Inicialización

```bash
# Crear directorio
mkdir my-mcp-server
cd my-mcp-server

# Inicializar virtualenv con uv
uv init
uv venv
source .venv/bin/activate  # En Windows: .venv\Scripts\activate
```

## Instalación del SDK

La librería principal es `mcp`.

```bash
uv add mcp
# O con pip
pip install mcp
```

## Estructura de Directorios

```text
my-mcp-server/
├── main.py        # Punto de entrada
├── pyproject.toml # Dependencias (si usas uv/poetry)
└── .venv/
```
