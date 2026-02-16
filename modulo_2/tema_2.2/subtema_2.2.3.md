# Subtema 2.2.3: Limitaciones del Transporte SSE y Motivación para Streamable HTTP

Aunque la arquitectura SSE+POST funciona y es compatible con cualquier servidor HTTP (Flask, Express, FastAPI), tiene desventajas significativas para sistemas distribuidos robustos.

## 1. Múltiples Conexiones

Requiere al menos dos conexiones TCP separadas (una de larga duración para SSE, y conexiones efímeras para cada POST). Esto aumenta la latencia y el consumo de recursos en firewalls y load balancers.

## 2. Problemas de "Sticky Sessions"

En un entorno de nube con balanceadores de carga (como AWS ALB), si tienes múltiples instancias de tu servidor:

- El `GET /sse` cae en el Servidor A.
- El `POST /message` cae en el Servidor B.

El Servidor B recibe el comando, pero no tiene el canal SSE abierto para responder al cliente. Esto obliga a usar "Sticky Sessions" (afinidad de sesión) o una capa de mensajería externa (Redis) para coordinar servidores, complicando la arquitectura.

## 3. Seguridad y CORS

Manejar CORS (Cross-Origin Resource Sharing) en dos endpoints con diferentes métodos y cabeceras puede ser propenso a errores de configuración.

## La Solución: Streamable HTTP (MCP 2.0)

Para resolver esto, la especificación evolucionó hacia **Streamable HTTP**, que veremos en el siguiente tema.
