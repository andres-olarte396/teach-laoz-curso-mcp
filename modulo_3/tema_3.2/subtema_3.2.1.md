# Subtema 3.2.1: Anotaciones de Herramientas: ReadOnly, Destructive y OpenWorld

No todas las herramientas son iguales. Leer un archivo es seguro; borrar una base de datos no lo es. MCP permite etiquetar tus herramientas para que el Host sepa cómo tratarlas.

## Anotaciones Soportadas

Aunque la especificación evoluciona, las anotaciones (hints) más comunes que los clientes respetan son:

### 1. `destructive` (Destructiva)

Indica que la herramienta tiene efectos secundarios irreversibles (borrar, modificar, gastar dinero).

- **Comportamiento del Host:** Probablemente mostrará una advertencia roja y exigirá confirmación explícita del usuario antes de ejecutarla.

### 2. `readOnly` (Solo Lectura)

Indica que la herramienta es segura y sin efectos secundarios.

- **Comportamiento del Host:** Puede ejecutarse automáticamente sin molestar al usuario.

### 3. `openWorld` (Mundo Abierto)

Indica que la herramienta puede hacer "cualquier cosa" (ej: ejecutar código arbitrario en shell).

- **Comportamiento del Host:** Tratar con máxima precaución.

## Implementación

Estás anotaciones se pasan en un campo `hints` o `tags` dentro de la definición de la herramienta (dependiendo de la versión del SDK/Spec). Un patrón común es usar tags en el nombre o descripción, pero la forma estructurada es:

```json
{
  "name": "delete_user",
  "description": "Elimina un usuario permanentemente",
  "inputSchema": {...},
  "tags": ["destructive"]
}
```
