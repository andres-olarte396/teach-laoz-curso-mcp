# Subtema 10.1.3: Patrón Gateway: Unificación de Endpoints

A veces no quieres que el Cliente sepa que existen N servidores. Quieres exponer un **único endpoint SSE**.

## Arquitectura

`Client <--> [ MCP Gateway ] <--> [ Server A, Server B, Server CD ]`

## Implementación

El Gateway es a la vez un **Servidor** (hacia el Cliente) y un **Cliente** (hacia los servidores backend).

1.  Recibe `list_tools` del Cliente.
2.  Hace `list_tools` a A, B y C.
3.  Combina las respuestas y responde al Cliente.
4.  Recibe `call_tool("serverA_tool", ...)`.
5.  Detecta el prefijo, le quita el namespace, y llama a Server A.
6.  Devuelve la respuesta.

Esto abstrae la complejidad y permite cambiar backends sin reconfigurar a los clientes.
