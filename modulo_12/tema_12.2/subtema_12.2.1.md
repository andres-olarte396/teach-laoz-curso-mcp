# Subtema 12.2.1: Arquitectura de Referencia y Pasos Sugeridos

No tienes que empezar desde cero. Aquí tienes una guía de arquitectura.

## Diagrama de Componentes

```mermaid
graph TD
    User((Usuario)) <--> Host[Ops Dashboard / Web Host]
    Host <--> LLM[OpenAI / Anthropic API]

    subgraph "MCP Layer"
        Host -- SSE + OAuth --> Gateway[MCP Gateway (Opcional)]
        Gateway --> S1[Server Monitor (Py)]
        Gateway --> S2[Server Docs (TS)]
        Gateway --> S3[Server DB (Py)]
    end

    S1 --> Logs[Log Files]
    S2 --> MD[Markdown Files]
    S3 --> SQLite[(SQLite DB)]
```

## Plan de Implementación Sugerido

### Día 1: Los Servidores

1.  Crea `ops-monitor` con FastMCP. Prueba con `mcp-inspector` que puedes leer logs.
2.  Crea `ops-db`. Define el esquema de tickets.
3.  Crea `ops-docs`. Añade 2 o 3 archivos md de ejemplo ("Cómo reiniciar nginx").

### Día 2: Integración

1.  Configura `claude_desktop_config.json` para probar los 3 servidores juntos con Claude.
2.  Verifica que Claude puede "Leer un error en logs -> Comprobar docs -> Reiniciar servicio -> Crear ticket".

### Día 3: El Cliente Custom

1.  Usa el SDK `client` en un script Node.js simple.
2.  Conecta a los 3 servidores.
3.  Implementa un bucle de chat simple en terminal.

### Día 4: Producción

1.  Escribe el `Dockerfile` para cada servidor.
2.  Crea el `docker-compose.yml`.
3.  Graba tu demo.
