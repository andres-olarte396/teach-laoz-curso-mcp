# Subtema 10.2.2: Sistemas Multi-Agente con Servidores Compartidos

En sistemas complejos, tienes varios agentes especializados (Coder, Reviewer, Manager).

## Arquitectura de Servidor Compartido

En lugar de que cada agente tenga sus propias herramientas hardcoded:

1.  Levantas un **Servidor MCP de Estado Compartido** (ej: Filesystem, Database).
2.  Conectas TODOS tus agentes a ese servidor MCP.

## Beneficio: Sincronización Gratis

Si el Agente Coder crea un archivo `main.py` usando `filesystem_server.write_file`, y luego el Agente Reviewer lee ese archivo con `filesystem_server.read_file`, ambos ven la misma versión de la realidad.

MCP actúa como el "bus de datos" o "pizarra compartida" para el equipo de agentes.
