# Subtema 0.3.1: Instalación de Node.js, Python y Gestores de Paquetes

## Node.js y npm

Node.js es fundamental para trabajar con el SDK de TypeScript y muchas herramientas del ecosistema.

1. **Descarga:** Ve a [nodejs.org](https://nodejs.org/) y descarga la versión LTS (Long Term Support).
2. **Verificación:**

   ```bash
   node -v
   npm -v
   ```

   Deberías ver versiones como `v18.x.x` o superior.

## Python y uv

Python es esencial para el desarrollo de servidores MCP en Python, especialmente para IA y Ciencia de Datos.

1. **Descarga:** Ve a [python.org](https://python.org/) y descarga Python 3.10 o superior.
2. **Gestor de paquetes `uv`:** Recomendamos encarecidamente usar `uv` (de Astral) en lugar de pip/venv estándar por su velocidad y manejo de proyectos.

   ```bash
   # En macOS/Linux
   curl -LsSf https://astral.sh/uv/install.sh | sh

   # En Windows (Powershell)
   powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```

3. **Verificación:**

   ```bash
   uv --version
   ```

## Git

Necesitarás Git para clonar repositorios y gestionar versiones.

1. **Descarga:** [git-scm.com](https://git-scm.com/).
2. **Configuración inicial:**

   ```bash
   git config --global user.name "Tu Nombre"
   git config --global user.email "tu@email.com"
   ```
