# Subtema 7.2.2: Retorno de Imágenes y Contenido Binario

MCP permite devolver imágenes para que el Host las muestre al usuario.

## Helper `Image`

FastMCP provee una clase helper para facilitar esto.

```python
from fastmcp import FastMCP, Image
import io
# Supongamos que usas PIL/Pillow
# from PIL import Image as PILImage

mcp = FastMCP("ImageServer")

@mcp.tool()
def generar_grafico() -> Image:
    """Genera un gráfico aleatorio."""

    # Lógica de generación (pseudo-código)
    # img = crear_grafico_matplotlib()
    # buf = io.BytesIO()
    # img.save(buf, format="PNG")
    # data = buf.getvalue()

    # Simulación de datos binarios
    data = b'\x89PNG\r\n...'

    return Image(data=data, format="png")
```

El Host recibirá el contenido en base64 y renderizará la imagen en el chat. Esto es ideal para herramientas de data science o generación de arte.
