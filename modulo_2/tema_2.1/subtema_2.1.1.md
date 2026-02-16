# Subtema 2.1.1: Modelo de Comunicación: stdin/stdout como Canal Bidireccional

## ¿Qué es stdio?

`stdio` (Standard Input/Output) es el mecanismo de comunicación más básico en sistemas operativos tipo Unix y Windows.
Cada proceso tiene, por defecto, tres canales:

1. **stdin (Entrada Estándar):** Donde el programa lee datos.
2. **stdout (Salida Estándar):** Donde el programa escribe datos (normalmente a la terminal).
3. **stderr (Error Estándar):** Donde el programa escribe errores o logs.

## stdio en MCP

MCP utiliza `stdio` para conectar un Host (ej: Claude Desktop) con un Servidor Local.

- El Host **lanza** el servidor como un subproceso.
- El Host **escribe** mensajes JSON-RPC en el `stdin` del servidor.
- El Servidor **lee** mensajes del `stdin`.
- El Servidor **escribe** respuestas JSON-RPC en su `stdout`.
- El Host **lee** las respuestas del `stdout` del servidor.

## Reglas Críticas

Para que esto funcione, hay una regla de oro:

> **El `stdout` debe usarse EXCLUSIVAMENTE para mensajes JSON-RPC.**

Si tu código hace `print("Hola mundo")` o `console.log("Depurando...")`, ese texto se mezclará con los mensajes JSON y romperá el parser del cliente.

### ¿Dónde loguear entonces?

Usa **`stderr`**. Todo lo que escribas en `stderr` será ignorado por el parser de protocolo MCP pero capturado por el Host como logs.

## Formato del Mensaje

Los mensajes se delimitan por **saltos de línea**.
Cada línea en stdout debe ser un objeto JSON-RPC completo y válido.

```text
{"jsonrpc":"2.0","method":"ping","id":1}\n
{"jsonrpc":"2.0","result":{},"id":1}\n
```
