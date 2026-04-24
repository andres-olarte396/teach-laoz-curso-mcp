# Guía de Estudio: Tema 7.1

Esta es la guía de estudio para los subtemas de esta sección. Utiliza este índice para navegar por los conceptos clave.

## Subtemas

### [Subtema 7.1.1: Instalación con uv y Configuración del Proyecto Python](./subtema_7.1.1.md)

> El ecosistema de Python para MCP ha adoptado herramientas modernas. Recomendamos usar uv (el sucesor espiritual de pip/poetry escrito en Rust) para la gestión de dependencias, aunque `pip` estándar también funciona.

### [Subtema 7.1.2: FastMCP: Decoradores @tool, @resource y @prompt](./subtema_7.1.2.md)

> Si vienes de FastAPI, te sentirás en casa. `FastMCP` es una capa de alto nivel sobre el SDK base que usa Type Hints de Python para generar todo automáticamente.

### [Subtema 7.1.3: Manejo de Tipos Complejos con Pydantic](./subtema_7.1.3.md)

> Para argumentos más complejos que un `int` o `str`, FastMCP se integra nativamente con Pydantic.

### [Subtema 7.1.4: Context: Acceso al Cliente, Logging y Progreso](./subtema_7.1.4.md)

> FastMCP inyecta automáticamente un objeto `Context` si lo declaras como argumento en tu función. Esto te da acceso a las capacidades del protocolo.
