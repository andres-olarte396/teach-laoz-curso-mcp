# Subtema 11.3.1: Versionado y Compatibilidad

Las APIs de herramientas evolucionan. ¿Qué pasa si cambias los argumentos de `create_user`?

## Estrategias

1.  **Nuevas Herramientas (Recomendado):**
    En lugar de cambiar `create_user`, crea `create_user_v2` y marca la anterior como `deprecated` en su descripción.
    _Descripción:_ "DEPRECATED: Use create_user_v2 instead. Crea un usuario..."

2.  **Argumentos Opcionales:**
    Si añades un campo, hazlo opcional. Nunca elimines campos obligatorios sin cambiar la versión mayor.

3.  **Negociación de Versión:**
    Usa la capacidad experimental `prompts/listChanged` o notificaciones para avisar al cliente que refresque su lista.
