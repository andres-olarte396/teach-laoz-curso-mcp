# Subtema 9.3.1: Validación y Sandboxing

No confíes en que el LLM te enviará argumentos bien formados.

## Validación Estricta

Usa `zod` (TS) o `Pydantic` (Py) siempre. No aceptes `any` ni `dict` genéricos.
Si esperas un path, usa validadores que aseguren que no contiene `../` (Path Traversal).

## Rate Limiting

Un servidor expuesto a internet debe limitar cuántas peticiones acepta por minuto para evitar DoS o costos excesivos de API (si tu herramienta llama a OpenAI).

## Sandboxing

Si tu herramienta ejecuta código (ej: un intérprete de Python):

1.  **Docker:** Ejecútalo en un contenedor efímero sin red.
2.  **WebAssembly:** Usa WASM para aislar la ejecución en memoria.
3.  **VM:** Nunca ejecutes `eval()` o `subprocess.run` directamente en el host productivo.
