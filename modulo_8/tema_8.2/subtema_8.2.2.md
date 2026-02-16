# Subtema 8.2.2: VS Code, Cursor y Windsurf

Los IDEs modernos están integrando MCP para dar superpoderes a sus asistentes de IA.

## Cursor

Cursor (un fork de VS Code con IA nativa) soporta MCP.

1.  Ve a **Cursor Settings** > **General** > **MCP**.
2.  Haz clic en **Add New MCP Server**.
3.  Introduce el nombre y el comando (ej: `uv run main.py`).

Ahora, cuando chatees con el modelo de Cursor (`Ctrl+L`), él podrá ver y llamar a tus herramientas.

## VS Code (Extensión)

Aunque VS Code nativo aún está integrando esto, existen extensiones como **"MCP Host"** que permiten conectar servidores.

## Windsurf

Windsurf (de Codeium) usa un sistema de "Cascadas" que es compatible conceptualmente, y están adoptando MCP activamente. La configuración suele ser vía un archivo YAML o UI similar a Cursor.

**Ventaja Clave:** Al conectar MCP a tu IDE, la IA no solo "escribe código", sino que puede "ejecutar acciones" (desplegar, consultar DBs, leer logs) directamente desde el editor.
