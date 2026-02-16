# Subtema 6.1.1: Instalación y Configuración del Proyecto TypeScript

Para construir servidores profesionales, TypeScript es el lenguaje de referencia en el ecosistema MCP debido a su tipado estricto que encaja perfectamente con JSON Schema.

## Prerrequisitos

- Node.js v18+
- npm o pnpm

## Inicialización del Proyecto

```bash
mkdir mi-servidor-mcp
cd mi-servidor-mcp
npm init -y
npm install typescript @types/node --save-dev
npx tsc --init
```

## Instalación del SDK

El SDK oficial se divide en paquetes modulares, pero para un servidor básico necesitamos:

```bash
npm install @modelcontextprotocol/sdk zod
```

_(Usamos `zod` porque facilita enormemente la definición de esquemas para las Tools)._

## Configuración `tsconfig.json`

Asegúrate de tener esto para evitar dolores de cabeza con módulos ESM:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "Node16",
    "moduleResolution": "Node16",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "skipLibCheck": true
  }
}
```

## Estructura de Directorios

```text
mi-servidor-mcp/
├── src/
│   └── index.ts
├── package.json
└── tsconfig.json
```
