# Subtema 6.4.4: Proyecto Práctico: Servidor MCP de API Gateway

El objetivo final de este módulo es construir un servidor robusto que unifique varias APIs.

## Requisitos del Proyecto

Crear un servidor `gateway-mcp` que:

1.  **Integración GitHub:**
    - Tool `get_issue(repo, id)`: Trae título y estado.
    - Resource `github://{repo}/readme`: Lee el README.md.

2.  **Integración JSON Placeholder (Mock API):**
    - Tool `get_todo(id)`: Trae un TODO de la API pública.

3.  **Autenticación:**
    - Leer `GITHUB_TOKEN` de variables de entorno. Fallar gracefully si falta.

4.  **Logging:**
    - Emitir log `info` cada vez que se llama a una API externa.

5.  **Tests:**
    - Un test unitario para la lógica de parseo de GitHub (mockeando la llamada HTTP real).
    - Un test E2E que verifique que el servidor arranca.

## Estructura Sugerida

```text
src/
  services/
    github.ts
    json-placeholder.ts
  tools/
    index.ts
  resources/
    index.ts
  index.ts
tests/
  unit/
  e2e/
```

Este proyecto consolida todo lo aprendido sobre TypeScript, estructura de proyectos, APIs y testing.
