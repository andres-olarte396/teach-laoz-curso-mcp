# Subtema 7.1.4: Context: Acceso al Cliente, Logging y Progreso

FastMCP inyecta automáticamente un objeto `Context` si lo declaras como argumento en tu función. Esto te da acceso a las capacidades del protocolo.

## Inyección de Contexto

```python
from fastmcp import FastMCP, Context

mcp = FastMCP("ContextDemo")

@mcp.tool()
async def proceso_largo(ctx: Context) -> str:
    """Una operación que reporta progreso y logs."""

    # 1. Logging
    ctx.info("Iniciando proceso...")

    # 2. Reporte de Progreso
    for i in range(10):
        await ctx.report_progress(i, total=10)
        # simular trabajo...

    # 3. Acceso al ID de request (útil para tracing)
    request_id = ctx.request_id

    return "Listo"
```

## Sampling desde Python

El contexto también permite pedir al Host que use su LLM (Sampling).

```python
@mcp.tool()
async def pedir_ayuda(tema: str, ctx: Context) -> str:
    """Pide al LLM del host que explique algo."""

    # Enviar mensaje de sampling
    result = await ctx.sample_llm(
        messages=[{"role": "user", "content": f"Explica brevemente {tema}"}],
        max_tokens=100
    )

    return f"El LLM dijo: {result.content}"
```

Esta integración hace que funciones avanzadas sean triviales de implementar.
