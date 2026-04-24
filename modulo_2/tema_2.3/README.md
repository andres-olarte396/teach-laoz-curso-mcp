# Guía de Estudio: Tema 2.3

Esta es la guía de estudio para los subtemas de esta sección. Utiliza este índice para navegar por los conceptos clave.

## Subtemas

### [Subtema 2.3.1: Arquitectura de Streamable HTTP](./subtema_2.3.1.md)

> Streamable HTTP es la evolución del transporte en MCP. En lugar de dos endpoints separados (SSE GET + POST), utiliza un enfoque unificado.

### [Subtema 2.3.2: Gestión de Sesiones: Mcp-Session-Id y Estado del Servidor](./subtema_2.3.2.md)

> Aunque Streamable HTTP intenta mantener una conexión persistente, en el mundo real las conexiones se cortan (timeout, cambio de red, reinicio de servidor).

### [Subtema 2.3.3: Resumability y Reconexión con Last-Event-ID](./subtema_2.3.3.md)

> La reconexión no es suficiente si se pierden mensajes durante el corte.

### [Subtema 2.3.4: Compatibilidad Retroactiva: Soporte Dual SSE y Streamable HTTP](./subtema_2.3.4.md)

> No todos los clientes soportan Streamable HTTP todavía. Para maximizar la compatibilidad, un servidor MCP moderno debería soportar ambos transportes.
