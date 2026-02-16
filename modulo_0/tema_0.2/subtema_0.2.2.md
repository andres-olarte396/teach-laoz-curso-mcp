# Subtema 0.2.2: El Problema de la Integración: Por Qué los LLMs Necesitan Herramientas

## Contexto Limitado

Los LLMs operan dentro de una "ventana de contexto". Solo pueden "ver" lo que tú les envías en el prompt. Si quieres que analicen un archivo de 1GB, no puedes simplemente pegarlo en el chat.

## Acceso a Datos Privados

Las empresas tienen terabytes de datos en bases de datos SQL, repositorios de documentos, CRMs y sistemas ERP. Los modelos públicos (como ChatGPT o Claude.ai) no tienen acceso a estos datos por razones obvias de seguridad y privacidad.

## Necesidad de Acción

Queremos que la IA no solo _hable_, sino que _haga_.

- "Reserva una reunión con Juan para el martes".
- "Reinicia el servidor de producción si el uso de CPU es > 90%".
- "Busca el último commit en el repo y despliégalo".

Para realizar estas acciones, el LLM necesita **herramientas**.

## ¿Qué es una Herramienta (Tool)?

En el contexto de IA, una herramienta es una función que el modelo puede "llamar".
El modelo no ejecuta la función. El modelo **genera los parámetros** para la función, y el sistema anfitrión (Host) ejecuta la función y le devuelve el resultado al modelo.

**Ejemplo:**

1. **Usuario:** "¿Qué tiempo hace en Madrid?"
2. **Modelo:** (Piensa: Necesito usar la herramienta `get_weather`) -> Genera llamada: `get_weather(city="Madrid")`.
3. **Sistema:** Ejecuta API del clima -> Recibe "25°C, Soleado".
4. **Sistema:** Pasa resultado al modelo.
5. **Modelo:** "En Madrid hace 25°C y está soleado."
