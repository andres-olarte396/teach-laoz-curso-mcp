# Subtema 2.4.1: Criterios de Selección: Cuándo Usar Qué Transporte

No hay un "mejor transporte" universal. Depende de tu caso de uso.

## Usar `stdio` cuando...

1.  **Desarrollo Local:** Estás creando y probando un servidor en tu propia máquina.
2.  **Seguridad Extrema:** No quieres exponer ningún puerto de red. Los datos nunca salen del proceso.
3.  **Simplicidad:** Quieres que tu servidor sea un simple script ejecutable sin dependencias de frameworks web.
4.  **Uso Personal:** Solo tú vas a usar este servidor con tu Claude Desktop.

## Usar `SSE` (Legacy) cuando...

1.  **Compatibilidad Amplia:** Necesitas soportar clientes MCP muy antiguos que no entienden Streamable HTTP.
2.  **Infraestructura Limitada:** Tu servidor web (ej: hosting PHP antiguo, o ciertos proxies corporativos) bloquea peticiones HTTP de larga duración bidireccionales pero permite SSE estándar.

## Usar `Streamable HTTP` cuando...

1.  **Producción Remota:** Despliegas tu servidor en la nube (AWS, GCP, Azure) para que lo usen múltiples personas.
2.  **Firewalls Estrictos:** Solo se permite tráfico saliente por puerto 443 estándar (sin Websockets).
3.  **Performance:** Necesitas la menor latencia posible en una conexión remota.
