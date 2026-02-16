# Subtema 11.3.2: Continuous Deployment (CI/CD)

Tu pipeline de despliegue debe garantizar que no rompes el contrato con el LLM.

## Pipeline Típico (GitHub Actions)

1.  **Lint & Type Check:** `uv run ruff check .` / `npm run lint`.
2.  **Unit Tests:** Ejecuta tests con `InMemoryTransport`.
3.  **Schema Validation:**
    Ejecuta un script que arranque el servidor, haga `list_tools` y verifique que los esquemas JSON de las herramientas son válidos y tienen descripciones útiles.
    _Tip:_ Falla el build si una herramienta no tiene descripción.
4.  **E2E Test:**
    Conecta un `stdio_client` real y verifica que el handshake completa en < 100ms.
5.  **Build & Push:** Construye la imagen Docker y súbela al registro.
6.  **Deploy:** Actualiza el Kubernetes Deployment.
