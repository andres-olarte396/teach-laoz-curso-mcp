# Subtema 8.3.3: Amazon Bedrock, Google AI y Otros Frameworks

La industria está convergiendo. Amazon Bedrock Agents y Google Vertex AI Agents soporte la invocación de herramientas externas.

## El Rol de MCP

MCP actúa como el "driver universal".
En lugar de escribir una integración específica para Bedrock, otra para Vertex y otra para OpenAI:

1.  Escribe tu herramienta **una vez** como servidor MCP.
2.  Usa un **Gateway MCP** (o un adaptador simple en Python/TS) que traduzca el protocolo a la API específica del proveedor cloud.

Esto protege tu inversión: si mañana cambias de AWS a Google, tus herramientas MCP siguen funcionando sin cambios.
