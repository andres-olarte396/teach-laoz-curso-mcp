# Subtema 10.3.2: Análisis de Servidores: Puppeteer

Uno de los servidores más potentes es `@modelcontextprotocol/server-puppeteer`.

## Capacidades

Expone herramientas para:

1.  `navigate(url)`: Ir a una página.
2.  `click(selector)`: Interactuar.
3.  `screenshot()`: Ver qué pasa (devuelve una imagen al chat).
4.  `evaluate(js)`: Ejecutar JS en la consola del navegador.

## Lección de Diseño

Este servidor es **stateful** (mantiene una sesión abierta de Chrome).
Si se reinicia el servidor MCP, se cierra el navegador. Esto es un ejemplo de diseño donde la conexión MCP está ligada al ciclo de vida del recurso externo.
