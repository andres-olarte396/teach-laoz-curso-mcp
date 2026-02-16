# Subtema 1.2.1: Los Tres Roles: Host, Client y Server

## Arquitectura de MCP

Para entender MCP, primero debemos identificar los actores. A menudo hablamos de "Cliente" y "Servidor", pero en MCP hay un tercer rol crucial: el "Host".

### 1. Host (Anfitrión)

El **Host** es la aplicación que el usuario final utiliza. Es donde "vive" la IA.

- **Responsabilidad:** Orquestar la conversación, gestionar la conexión con el LLM, y mostrar la interfaz de usuario.
- **Ejemplos:** Claude Desktop, VS Code (con extensión IA), Cursor, Zed.

### 2. Client (Cliente MCP)

El **Client** es el componente de software dentro del Host que habla el protocolo MCP. Mantiene una conexión 1:1 con el servidor.

- **Responsabilidad:** Enviar solicitudes al servidor (ej: `tools/list`, `tools/call`) y recibir respuestas.

> **Nota:** A menudo, "Host" y "Client" se usan indistintamente porque están empaquetados juntos, pero técnicamente el Client es el módulo de conectividad del Host.

### 3. Server (Servidor MCP)

El **Server** es el programa que expone las capacidades (Tools, Resources, Prompts).

- **Responsabilidad:** Ejecutar la lógica de negocio (consultar BD, leer archivos) y devolver resultados al Client.
- **Ejemplos:** `mcp-server-git`, `mcp-server-postgres`, tu propio script de Python.

## Diagrama de Interacción

```mermaid
graph LR
    User[Usuario] -- Interfaz --> Host[Host (Claude Desktop)]
    Host -- Prompt + Contexto --> LLM[Modelo (Claude 3.5)]
    Host -- Protocolo MCP --> Server[Servidor MCP (Postgres)]

    subgraph "Mundo MCP"
    Client[Cliente MCP (Integrado en Host)] <--> Server
    end
```

## Flujo Típico

1. **Host** inicia el **Server** (usualmente como un subproceso).
2. **Client** y **Server** realizan un "handshake" para acordar versiones y capacidades.
3. **Host** pregunta al **LLM**: "¿Qué quieres hacer?".
4. **LLM** responde: "Quiero usar la herramienta `query_users`".
5. **Host** usa su **Client** para enviar un mensaje `tools/call` al **Server**.
6. **Server** ejecuta la consulta SQL y devuelve el resultado JSON.
7. **Host** pasa el resultado al **LLM**.
8. **LLM** genera la respuesta final al usuario.
