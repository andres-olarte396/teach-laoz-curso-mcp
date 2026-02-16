# Subtema 5.1.3: Human-in-the-Loop: Consentimiento y Modificación

Sampling es poderoso, pero también invasivo. Un servidor malicioso podría usar tu LLM para generar spam o minar tokens.

## El Principio de Consentimiento

El protocolo MCP estipula que el **Usuario es Soberano**.

Cuando llega una petición `sampling/createMessage`, el Host (ej: Claude Desktop) tiene varias opciones:

1.  **Aprobación Silenciosa:** Si el usuario confía plenamente en el servidor (ej: servidor local propio), el Host ejecuta el sampling sin preguntar.
2.  **Aprobación Explícita:** El Host muestra un pop-up: _"El servidor X quiere generar texto. Ver prompt / Aprobar / Rechazar"_.
3.  **Modificación:** El usuario puede **editar** el prompt antes de que vaya al LLM.

## Diseño Resiliente

Tu servidor debe estar preparado para ser **rechazado**.

```python
try:
    result = await ctx.sampling.create_message(...)
except McpError as e:
    if e.code == -1: # Usuario rechazó
        return "No pude arreglar el código porque no se autorizó el uso del modelo."
```

Nunca asumas que el sampling tendrá éxito. Diseña tus herramientas para degradarse elegantemente si el humano dice "No".
