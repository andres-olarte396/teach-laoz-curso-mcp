# Subtema 10.2.3: MCP vs Protocolos Agent-to-Agent (A2A)

Existen protocolos para que los agentes "hablen entre sí" (como el chat). MCP no es eso.

## Diferencias

| Protocolo | Rol                                   | Comunicación      | Ejemplo                                  |
| :-------- | :------------------------------------ | :---------------- | :--------------------------------------- |
| **MCP**   | Conectar IA con Sistemas (Tools/Data) | Client <-> Server | "Lee este archivo", "Ejecuta SQL"        |
| **A2A**   | Conectar IA con IA (Coordinación)     | Agent <-> Agent   | "Revisa mi código", "Asigname una tarea" |

## Arquitectura Híbrida

La arquitectura ideal usa ambos:

- Los Agentes usan **A2A** para coordinar el trabajo ("Te paso el ticket #123").
- Los Agentes usan **MCP** para ejecutar el trabajo ("Leo la DB para el ticket #123").

No trates de forzar a MCP para ser un protocolo de chat entre agentes.
