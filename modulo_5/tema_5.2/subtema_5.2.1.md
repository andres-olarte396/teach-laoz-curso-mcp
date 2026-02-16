# Subtema 5.2.1: Qué Son los Roots y Para Qué Sirven

Hasta ahora, hemos visto cómo el servidor expone cosas al Host. **Roots** es lo opuesto: el Host informa al servidor sobre el entorno del usuario.

## El Problema del Contexto

Imagina que tienes un servidor `git-mcp` que puede hacer commits. Pero, ¿en qué repositorio?

El usuario podría tener 10 proyectos abiertos en VS Code. El servidor necesita saber **cuáles son las carpetas raíz** activas en el editor para ofrecer contexto relevante.

## La Solución: Roots

Un **Root** es simplemente una URI que apunta a un directorio o recurso que el usuario considera "activo" o "parte de su espacio de trabajo actual".

- En VS Code: Las carpetas abiertas en el Explorer.
- En Claude Desktop: Carpetas añadidas manualmente a la configuración.

## Seguridad

Los Roots también actúan como una **lista blanca de seguridad**.
Un servidor bien comportado solo debería acceder a archivos dentro de los Roots listados, y rechazar peticiones fuera de ellos (evitando Path Traversal accidental).
