# Subtema 1.4.2: Especificación 2025-03-26: Streamable HTTP y OAuth

Esta actualización mayor (a menudo referida como MCP 2.0) transformó el protocolo de "local-first" a "remote-ready".

## Streamable HTTP

Se introdujo un nuevo transporte que permite comunicación bidireccional eficiente sobre una sola conexión HTTP, simplificando drásticamente el despliegue en la nube (AWS Lambda, Cloudflare Workers).

## OAuth 2.1

Se estandarizó el flujo de autenticación, permitiendo que:

1. El Host redirija al usuario a una página de login.
2. El Servidor emita tokens de acceso seguros.
3. El Host use esos tokens para invocar herramientas.

Esto hizo posible conectar MCP a servicios corporativos sensibles (Salesforce, SAP).
