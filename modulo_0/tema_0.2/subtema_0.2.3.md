# Subtema 0.2.3: Panorama de Soluciones: Function Calling, Tool Use y Protocolos Abiertos

## Function Calling (OpenAI)

OpenAI popularizó el concepto de "Function Calling". Permite definir funciones en formato JSON Schema que el modelo puede optar por utilizar.

**Problema:** Cada proveedor (OpenAI, Anthropic, Google, Mistral) tiene su propia forma ligeramente diferente de implementar esto.

## Tool Use (Anthropic)

Anthropic tiene su propia API de "Tool Use", muy robusta, pero específica para sus modelos Claude.

## El Problema N×M

Imagina que quieres conectar 3 herramientas (Google Drive, Slack, GitHub) a 3 clientes de IA diferentes (Claude Desktop, VS Code AI, ChatGPT).

- Sin un estándar, tendrías que escribir una integración específica para cada par Herramienta-Cliente.
- Con 10 herramientas y 10 clientes, necesitarías **100 integraciones**.

## La Solución: Protocolos Abiertos (MCP)

El **Model Context Protocol (MCP)** nace para resolver este problema creando un estándar universal.

- **Un solo protocolo** para definir herramientas.
- Cualquier **Cliente MCP** (Host) puede usar cualquier **Servidor MCP**.
- Escribes la integración **una vez** (como servidor MCP) y funciona en Claude, en IDEs, y en cualquier futuro agente de IA.

MCP no reinventa el "Function Calling", sino que lo estandariza y lo desacopla del modelo específico, añadiendo además capacidades de gestión de contexto (Recursos) y Prompts.
