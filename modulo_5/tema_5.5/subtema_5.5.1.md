# Subtema 5.5.1: Concepto de Recursos Virtuales

Hasta ahora hemos tratado los `Resources` como si fueran archivos reales en el disco (`file:///var/log/syslog`).
Pero MCP no obliga a que un recurso corresponda a un archivo físico.

## ¿Qué es un Recurso Virtual?

Un Recurso Virtual es un dato generado dinámicamente por el servidor en el momento de la lectura, pero presentado al LLM con una URI que parece un archivo.

### Ejemplos

1.  **Base de Datos como Archivos:**
    - URI: `postgres://users/1.json`
    - Al leerlo, el servidor hace `SELECT * FROM users WHERE id=1` y devuelve el JSON.
    - Para el LLM, es solo un archivo JSON más.

2.  **API Externa como Archivos:**
    - URI: `github://repo/issues/latest.md`
    - Al leerlo, el servidor llama a la API de GitHub, obtiene los últimos issues y genera un reporte Markdown on-the-fly.

3.  **Estado del Sistema:**
    - URI: `system://cpu/usage`
    - Devuelve "45%" calculado en tiempo real.

## ¿Por qué Virtualizar?

La ventaja principal es la **Abstracción Uniforme**.

El LLM sabe muy bien cómo "leer archivos". Si abstraemos la complejidad de SQL, APIs HTTP y comandos de sistema detrás de una interfaz simple de lectura de recursos, facilitamos enormemente el trabajo del modelo.

En lugar de enseñarle a usar una herramienta compleja `sql_query(query="SELECT...")`, simplemente le decimos: "Lee el archivo `db://users/1`".
