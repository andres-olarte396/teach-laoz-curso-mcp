# Subtema 3.3.1: Granularidad: Herramientas Atómicas vs Herramientas Compuestas

Diseñar la granularidad correcta es un arte.

## Herramientas Atómicas (Recomendado)

Una herramienta hace **una sola cosa** bien.

- Ejemplo: `get_user_by_id`, `update_user_email`, `send_welcome_email`.
- **Ventaja:** El LLM puede componer flujos complejos. ("Busca al usuario 1, actualiza su email, y envíale un correo").
- **Desventaja:** Requiere múltiples round-trips (llamadas) para completar una tarea.

## Herramientas Compuestas (Macro)

Una herramienta hace **todo un proceso de negocio**.

- Ejemplo: `onboard_new_user` (que internamente crea el usuario, envía email, asigna rol, etc.).
- **Ventaja:** Eficiencia (1 llamada). Garantía transaccional.
- **Desventaja:** Menos flexible. El LLM no puede variar el proceso.

## Regla de Oro

Empieza con herramientas atómicas. Solo crea compuestas si detectas que el LLM siempre realiza la misma secuencia de 5 pasos y se equivoca a menudo.
