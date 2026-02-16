# Subtema 11.1.3: Alertas y Respuesta a Incidentes

Configura alertas para no tener que mirar los dashboards todo el día.

## Alertas Recomendadas

1.  **High Error Rate:** Si > 5% de las llamadas a `query_database` fallan en 5 minutos -> PagerDuty.
2.  **High Latency:** Si p99 de `fast_tool` > 2s -> Slack Warning.
3.  **Server Down:** Si el healthcheck `/healthz` no responde.

## Dashboards de Agente

Crea un dashboard que muestre:

- Top Tools usadas.
- Top Usuarios (si tienes auth).
- Tokens consumidos (si integras con un LLM de pago dentro de la tool).
