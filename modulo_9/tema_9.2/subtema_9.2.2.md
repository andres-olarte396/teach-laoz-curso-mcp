# Subtema 9.2.2: Server Metadata Discovery y Registro Dinámico

Para que el Host sepa cómo autenticarte, debes exponer metadatos estándar (RFC 8414).

## El Endpoint `/.well-known/oauth-authorization-server`

Tu servidor debe responder a esta ruta con un JSON:

```json
{
  "issuer": "https://mi-servidor-mcp.com",
  "authorization_endpoint": "https://mi-servidor-mcp.com/auth",
  "token_endpoint": "https://mi-servidor-mcp.com/token",
  "scopes_supported": ["mcp:connect"],
  "response_types_supported": ["code"],
  "grant_types_supported": ["authorization_code"],
  "code_challenge_methods_supported": ["S256"]
}
```

## Registro Dinámico (RFC 7591)

Si quieres permitir que cualquier cliente se conecte sin registro previo manual, puedes implementar un endpoint de registro.

Claude Desktop (y otros clientes) intentarán registrarse automáticamente enviando sus metadatos (nombre, logo, redirect URIs) para obtener un `client_id` al vuelo.
