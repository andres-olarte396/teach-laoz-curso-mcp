# Subtema 7.3.2: Consumo de Tools, Resources y Prompts desde Python

Una vez conectado, `session` expone métodos asíncronos para interactuar.

## Invocando Herramientas

```python
# Llamada a herramienta 'sumar'
result = await session.call_tool(
    name="sumar",
    arguments={"a": 10, "b": 20}
)

# El resultado es un objeto CallToolResult
content = result.content[0]
if content.type == "text":
    print(f"Resultado: {content.text}")
```

## Leyendo Recursos

```python
# Listar recursos disponibles
resources = await session.list_resources()

# Leer el primero
if resources.resources:
    uri = resources.resources[0].uri
    data = await session.read_resource(uri)
    print(f"Contenido de {uri}: {data.contents[0].text}")
```

## Usando Prompts

```python
# Obtener un prompt renderizado
prompt = await session.get_prompt(
    name="revisar_codigo",
    arguments={"codigo": "print('hola')"}
)

# 'prompt' contiene una lista de mensajes listos para enviar a tu LLM favorito
print(prompt.messages)
```

La API es consistente y tipada, lo que facilita la integración en scripts de automatización o agentes.
