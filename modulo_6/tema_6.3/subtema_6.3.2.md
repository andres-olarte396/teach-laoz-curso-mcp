# Subtema 6.3.2: Invocación de Herramientas y Lectura de Recursos

Una vez conectado, usar el servidor es trivial.

## Llamar a una Herramienta (`callTool`)

```typescript
try {
  const result = await client.callTool({
    name: "get_weather",
    arguments: {
      city: "Madrid",
    },
  });

  // Procesar resultado
  if (result.isError) {
    console.error("Error lógico en la herramienta:", result.content);
  } else {
    console.log("Resultado:", result.content);
  }
} catch (error) {
  console.error("Error de protocolo o transporte:", error);
}
```

## Leer un Recurso (`readResource`)

```typescript
const resources = await client.listResources();
const firstUri = resources.resources[0].uri;

const content = await client.readResource({ uri: firstUri });
console.log("Contenido del recurso:", content.contents[0].text);
```

El SDK tipado de TypeScript hace que estos métodos sean muy seguros y fáciles de usar con autocompletado del IDE.
