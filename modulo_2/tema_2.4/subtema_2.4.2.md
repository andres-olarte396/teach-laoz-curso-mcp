# Subtema 2.4.2: Patrones de Despliegue Comunes

## 1. El Sidecar Local (stdio)

El patrón más común para desarrolladores.

- El Host y el Servidor corren en la misma máquina.
- No hay latencia de red.
- Ideal para acceder a archivos locales o bases de datos locales (SQLite).

## 2. El Gateway Remoto (HTTP)

Para equipos y organizaciones.

- Un servidor central corre en Kubernetes/Docker.
- Expone una API HTTP (Soporte Dual).
- Los desarrolladores conectan sus Hosts locales (Claude Desktop) a este servidor remoto.
- **Seguridad:** Requiere autenticación (OAuth 2.1) porque está expuesto a internet/intranet.

## 3. Serverless (AWS Lambda / Vercel Functions)

Gracias a Streamable HTTP, MCP funciona excelente en Serverless.

- El servidor "duerme" hasta que recibe una petición.
- **Reto:** El estado de la sesión debe guardarse externamente (Redis/DynamoDB) porque la función lambda muere después de responder.
- **Ventaja:** Costo cero cuando nadie lo usa.
