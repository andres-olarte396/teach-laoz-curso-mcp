# Subtema 10.1.1: Patrón Aggregator: Un Cliente, Múltiples Servidores

![Patrón Aggregator](../../../diagramas/modulo_10/patron_aggregator.svg)

Este es el patrón más simple y común. El Host (ej: Claude Desktop) actúa como un **Aggregator**.

## Funcionamiento

1.  El Host lee su configuración (`claude_desktop_config.json`) y ve 5 servidores definidos.
2.  Lanza 5 conexiones independientes en paralelo.
3.  Hace `list_tools` a cada uno.
4.  Une todas las herramientas en una sola lista plana (o agrupada por UI).
5.  Se la presenta al LLM como si fuera un solo "Super Servidor".

## Ventajas

- Aislamiento total: Si un servidor falla, los otros siguen funcionando.
- Simplicidad: No hay un componente intermedio que mantener.

## Código (Conceptual en TS)

```typescript
const servers = [serverA, serverB, serverC];
const aggregator = new AggregatorClient();

await Promise.all(servers.map((s) => aggregator.connect(s)));

const allTools = aggregator.listTools();
// [ {name: "toolA", ...}, {name: "toolB", ...} ]
```

