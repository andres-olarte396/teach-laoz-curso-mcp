# Subtema 10.1.2: Enrutamiento y Resolución de Conflictos

Cuando conectas múltiples servidores, surge un problema: ¿Qué pasa si dos servidores tienen una herramienta llamada `search`?

## Estrategias de Namespacing

### 1. Prefijado Automático (Recomendado)

El Host añade el nombre del servidor al nombre de la herramienta.

- Server "`marketing`" -> tool "`get_metrics`" -> ID: `marketing__get_metrics`.
- Server "`sales`" -> tool "`get_metrics`" -> ID: `sales__get_metrics`.

Esto garantiza unicidad.

### 2. Router Inteligente

Un componente intermedio (Gateway) recibe la petición `search` y decide a quién enviarla basándose en el contexto o argumentos. Esto es complejo y propenso a errores.

## Enrutamiento de Prompts

Los prompts también se agregan.

- `marketing/campaign-ideas`
- `sales/pitch-draft`

El usuario (o el LLM) selecciona explícitamente qué prompt usar, por lo que las colisiones son menos problemáticas que en las tools automáticas.
