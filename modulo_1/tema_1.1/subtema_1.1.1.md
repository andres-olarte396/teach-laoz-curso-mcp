# Subtema 1.1.1: Historia de MCP: De Anthropic al Estándar Abierto

## El Origen

El **Model Context Protocol (MCP)** fue presentado al mundo por **Anthropic** el 25 de noviembre de 2024. Nació de una observación simple pero frustrante: cada vez que una empresa quería conectar sus datos a una IA, tenía que construir una integración a medida.

## La Era Pre-MCP (Silos de Integración)

Antes de MCP, si querías que Claude accediera a tu Google Drive, Anthropic tenía que construir esa integración. Si querías que accediera a Slack, otra integración. Y si OpenAI quería hacer lo mismo, tenían que construir sus propias versiones.

Esto escalaba mal. Era el **problema N×M** en su máxima expresión.

## El Lanzamiento y la Visión

Anthropic lanzó MCP no como un producto propietario, sino como una **especificación abierta**.

> _"MCP es un estándar abierto que permite a los desarrolladores construir conexiones seguras y bidireccionales entre sus datos y las herramientas de IA."_

Desde el día 1, se publicaron SDKs para TypeScript y Python, junto con servidores de ejemplo para Google Drive, Slack y GitHub.

## Evolución Rápida

- **Noviembre 2024:** Lanzamiento inicial (Spec v0.1).
- **Diciembre 2024 - Febrero 2025:** Adopción rápida por parte de la comunidad. IDEs como Cursor, Windsurf y Zed anuncian soporte nativo.
- **Marzo 2025:** Se introduce soporte robusto para **OAuth** y transporte HTTP streamable, permitiendo servidores remotos seguros.

Hoy, MCP es un estándar _de facto_ para la interoperabilidad en la era de la IA, soportado por múltiples modelos y plataformas, no solo Anthropic.
