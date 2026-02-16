# Subtema 9.1.4: DNS Rebinding y Session Hijacking

Si ejecutas un servidor MCP localmente que escucha en HTTP (`localhost:8080`), eres vulnerable a ataques desde el navegador.

## DNS Rebinding

1.  Visitas `website-malicioso.com`.
2.  El sitio tiene un DNS que resuelve a su IP por un segundo, y luego cambia a `127.0.0.1` (tu localhost).
3.  El JS del sitio malicioso hace peticiones a `website-malicioso.com:8080`.
4.  Tu navegador cree que habla con el sitio remoto, pero en realidad está hablando con tu servidor MCP local.
5.  El atacante puede ejecutar herramientas en tu máquina.

## Prevención

- **Autenticación Obligatoria:** Los servidores MCP HTTP deben requerir un token de autenticación (incluso en localhost).
- **Validación de Host Header:** El servidor debe rechazar peticiones donde el header `Host` no sea `localhost` o `127.0.0.1`.
