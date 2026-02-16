# Subtema 11.2.1: Stateless vs Stateful

La decisión de arquitectura más importante.

## Stateless (Recomendado)

El servidor no recuerda interacciones pasadas. Cada `call_tool` es independiente.

- **Escalabilidad:** Trivial. Levanta 10 réplicas y pon un Load Balancer delante.
- **Ejemplo:** Un servidor de conversión de unidades o de consulta a una API pública.

## Stateful

El servidor mantiene contexto (ej: conexión a una sesión de navegador Puppeteer, conexión a BD transaccional).

- **Problema:** Si el usuario A está "en el servidor 1", el siguiente request debe ir al servidor 1 (Sticky Sessions).
- **Solución:** Externalizar el estado (Redis, Database) para volver a ser Stateless.

> **Consejo:** Diseña tus servidores MCP para ser Stateless siempre que sea posible.
