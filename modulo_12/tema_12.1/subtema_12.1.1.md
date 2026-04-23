# Subtema 12.1.1: Especificaciones del Proyecto Final: "Ecosistema de Operaciones Inteligentes"

Bienvenidos al desafío final. Aquí demostrarás que dominas el Protocolo de Contexto de Modelo (MCP) construyendo un sistema completo.

## El Escenario

Eres el Lead Architect de una startup que quiere revolucionar DevOps. Tu tarea es construir un **"Ecosistema de Operaciones Inteligentes"** donde un LLM pueda diagnosticar, arreglar y documentar incidencias en servidores.

## Requisitos Funcionales

Debes implementar **3 Servidores MCP** y **1 Cliente/Host**:

1. **Servidor 1: `ops-monitor` (Python/FastMCP)**
    - **Resources:** `logs://system/{date}` (Lee logs simulados), `metrics://cpu` (Stream de métricas).
    - **Tools:** `check_status(service_name)`, `restart_service(service_name)`.

2. **Servidor 2: `ops-docs` (Node.js/SDK)**
    - **Resources:** Documentación técnica en Markdown.
    - **Prompts:** `generate_incident_report`.
    - **Tools:** `search_docs(query)`.

3. **Servidor 3: `ops-db` (Tu elección)**
    - **Tools:** `create_ticket(title, severity)`, `list_tickets()`.
    - Base de datos SQLite real.

4. **Cliente Custom: `ops-dashboard`**
    - Una pequeña web o CLI que se conecte a los 3 servidores (vía Gateway o Directo).
    - Permita al usuario chatear con "OpsBot" para resolver problemas usando las herramientas.

## Requisitos No Funcionales

- **Seguridad:** El servidor `monitor` debe requerir confirmación para `restart_service`.
- **Logging:** Todos las llamadas a herramientas deben quedar registradas.
- **Docker:** Todo el sistema debe levantarse con un solo `docker-compose up`.
