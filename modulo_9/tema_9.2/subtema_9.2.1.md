# Subtema 9.2.1: El Framework de Autorización MCP: OAuth 2.1

![Flujo OAuth 2.1](../../../diagramas/modulo_9/oauth2_flujo.svg)

Para conectarse a **servidores remotos** sobre HTTP, MCP estandariza el uso de **OAuth 2.1**.

## Roles

1.  **Client:** El Host (ej: Claude Desktop).
2.  **Resource Server:** Tu servidor MCP.
3.  **Authorization Server (AS):** Quien emite los tokens (ej: Auth0, GitHub, o tu propio servicio).

> **Nota:** En configuraciones simples, el Resource Server y el Authorization Server pueden ser la misma aplicación.

## Flujo (Authorization Code Flow with PKCE)

1.  **Discovery:** El Cliente descarga `/.well-known/oauth-authorization-server` para saber dónde loguearse.
2.  **Authorization Request:** El Cliente abre el navegador del usuario en la URL de login.
3.  **User Consent:** El usuario se loguea y aprueba el acceso.
4.  **Token Exchange:** El Cliente intercambia el código de autorización por un Access Token.
5.  **MCP Connection:** El Cliente abre la conexión SSE enviando el token en el header `Authorization: Bearer <token>`.

Esto evita que el usuario tenga que copiar y pegar API Keys manualmente.

