# Subtema 7.4.2: Deployment: stdio, SSE y Streamable HTTP

Tu servidor FastMCP es políglota en transportes.

## 1. stdio (Por defecto)

Ideal para uso local con Claude Desktop o IDEs.

```bash
python main.py
```

FastMCP detecta si es una terminal interactiva o no, y actúa en consecuencia.

## 2. SSE (Server-Sent Events)

Para exponer tu servidor a la red (ej: desarrollo remoto).

```bash
mcp run main.py --transport sse --port 8000
```

Esto levanta un servidor uvicorn/starlette automáticamente.

## 3. Integración Manual en FastAPI

Si ya tienes una app FastAPI y quieres montar MCP en `/mcp`.

```python
from fastapi import FastAPI
from mcp.server.sse import SseServerTransport
from my_server import mcp # Tu instancia FastMCP

app = FastAPI()

@app.get("/sse")
async def handle_sse(request):
    # Lógica de adaptador (requiere un poco más de boilerplate actualmente)
    pass
```

FastMCP está evolucionando para hacer `app.mount(mcp)` posible en frameworks web con una sola línea.
