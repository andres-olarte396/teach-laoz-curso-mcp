# Subtema 10.3.3: Empaquetado y Publicación

Si creas un servidor útil, compártelo.

## Empaquetado

### Python

Usa `uv` o `poetry` para generar un paquete instalable.
Asegúrate de definir un `[project.scripts]` en `pyproject.toml` para que se pueda ejecutar como comando CLI: `mcp-server-demo`.

### Node.js

Usa `npm publish`.
Define `"bin": "./dist/index.js"` en `package.json`.

## Best Practices

1.  **README:** Explica claramente qué Tools y Resources expone.
2.  **Config:** Documenta las variables de entorno (`API_KEY`) necesarias.
3.  **Docker:** Ofrece una imagen Docker para facilitar el despliegue en la nube.
