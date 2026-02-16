# Subtema 9.2.4: Third-Party Authorization y Delegación

A menudo no quieres ser tú el Identity Provider. Quieres que el usuario se loguee con **GitHub** o **Google**.

## Flujo Delegado

1.  Tu servidor actúa como un **Authorization Server Facade**.
2.  Cuando el cliente pide autorizar, tu endpoint `/auth` redirige a GitHub (`https://github.com/login/oauth/authorize`).
3.  GitHub devuelve el usuario a tu `/callback`.
4.  Tú emites tu propio Access Token (o pasas el de GitHub encapsulado) al Cliente MCP.

Este patrón "Backend-for-Frontend" (BFF) es ideal para MCP porque mantiene al Cliente (Claude) agnóstico de si usas GitHub, Auth0 o Cognito. El Cliente solo habla OAuth estándar con tu servidor.
