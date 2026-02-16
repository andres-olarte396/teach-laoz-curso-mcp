# Subtema 5.1.1: El Flujo Inverso: Cuando el Servidor Necesita al LLM (Sampling)

Hasta ahora, todo ha sido:
`Usuario -> Host -> LLM -> Tool -> Servidor`

Pero, ¿qué pasa si el **Servidor** necesita la inteligencia del LLM para completar una tarea interna?

## El Problema

Imagina una herramienta `auto_fix_code`.

1.  Servidor recibe código roto.
2.  Servidor corre linter y ve errores.
3.  Servidor quiere _pensar_ cómo arreglarlo usando un modelo de lenguaje.

Sin Sampling, el servidor tendría que tener su propia API Key de OpenAI/Anthropic hardcodeada. Esto es malo (costoso, inseguro).

## La Solución: Sampling (`sampling/createMessage`)

MCP permite que el servidor le diga al Host:
_"Oye, ya que tienes un LLM potente conectado, ¿puedes procesar este prompt por mí y devolverme el texto generado?"_

Esto reutiliza la conexión y autenticación del usuario, manteniendo el control y la privacidad en el Host.

## Flujo

1.  **Servidor:** Envía `sampling/createMessage` al Host.
2.  **Host:** (Opcional) Pide permiso al usuario: "El servidor 'CodeFixer' quiere usar el modelo para generar código. ¿Permitir?".
3.  **Host:** Envía el prompt al LLM.
4.  **LLM:** Genera respuesta.
5.  **Host:** Envía respuesta al Servidor.
6.  **Servidor:** Usa el texto generado para finalizar su tarea.
