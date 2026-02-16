# Subtema 1.4.1: Especificación 2024-11-05: La Base Fundacional

Esta fue la primera versión estable (1.0) lanzada públicamente.

## Características Principales

- **Transporte stdio:** Enfocado en ejecución local.
- **Transporte SSE (Básico):** Soporte inicial para HTTP unidireccional.
- **Herramientas, Recursos y Prompts:** Las tres primitivas básicas bien definidas.
- **Sampling:** Capacidad básica para que el servidor "pida ayuda" al LLM.

## Limitaciones

- La comunicación remota era compleja debido a la naturaleza unidireccional de SSE.
- No había un estándar claro para autenticación (OAuth).
