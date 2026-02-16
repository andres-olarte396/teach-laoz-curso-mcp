# Subtema 11.2.2: Docker y Kubernetes

Desplegar servidores MCP en contenedores es el estándar.

## Dockerfile Ejemplo (Python uv)

```dockerfile
FROM python:3.11-slim
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/uv

WORKDIR /app
COPY pyproject.toml uv.lock .
RUN uv sync --frozen --no-install-project

COPY . .

# Exponer el puerto SSE
EXPOSE 8000
CMD ["uv", "run", "main.py", "--transport", "sse", "--port", "8000"]
```

## Kubernetes Deployment

Define un `Deployment` con 3 réplicas y un `Service` que exponga el puerto 8000.
Importante: Configura `readinessProbe` apuntando a tu endpoint de salud (si lo tienes) o verificando que el puerto TCP responde.
