# Subtema 9.1.1: Superficie de Ataque: Host, Client y Server

![Superficie de Ataque](../../../diagramas/modulo_9/superficie_ataque.svg)

MCP conecta sistemas locales con LLMs remotos y servicios externos. Esto crea una superficie de ataque única.

## Componentes Vulnerables

1.  **El Host (Client):** Tiene las credenciales del usuario, tokens de API y acceso a archivos locales. Si se compromete, el atacante lo tiene todo.
2.  **El Servidor:** Ejecuta código arbitrario. Si es malicioso o tiene bugs, puede abusar de los permisos que le da el Host.
3.  **El LLM:** Puede ser manipulado (Prompt Injection) para engañar al usuario o al servidor.
4.  **El Transporte:** Si usas HTTP/SSE sin cifrado (TLS), cualquiera en la red puede leer tus prompts y respuestas (MITM).

## Regla de Oro

> **"Trata a cada Servidor MCP como si fuera código no confiable descargado de Internet."**

Nunca conectes un servidor de terceros sin auditarlo, especialmente si tiene herramientas con efectos secundarios (`destructive`).

