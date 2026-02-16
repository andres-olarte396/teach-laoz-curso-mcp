# Subtema 6.4.1: MCP Inspector: Debugging Interactivo

El **MCP Inspector** es una herramienta dev-tool oficial (web-based) para depurar servidores sin necesidad de un LLM.

## Instalación y Uso

Se ejecuta directamente con `npx`, pasando el comando de tu servidor como argumento.

```bash
npx @modelcontextprotocol/inspector node dist/index.js
```

Esto abrirá una interfaz web en `http://localhost:5173` (puerto variable).

## Características

1.  **Explorador de Recursos:** Muestra la lista de recursos y permite leerlos.
2.  **Tester de Herramientas:** Formulario para rellenar argumentos y ejecutar herramientas.
3.  **Tester de Prompts:** Previsualiza el resultado de un prompt renderizado.
4.  **Log Viewer:** Muestra los logs en tiempo real enviados por el servidor.

Es el equivalente a "Postman" para APIs REST, pero para MCP.
