---
title: json-render
url: https://github.com/vercel-labs/json-render
tags: [frontend, generative, framework, typescript, vercel, apache-2.0]
added: 2026-09-23
added_by: Emiliano
---

Framework de "Generative UI" de Vercel Labs: el LLM genera un spec JSON restringido a un catálogo de componentes que vos definís con Zod, y un renderer lo dibuja en streaming mientras llega. El modelo no escribe código de UI: sólo arma piezas que ya existen.

## Por qué vale la pena

- **La UI queda acotada**: `defineCatalog(schema, {components, actions})` define qué puede usar el modelo, `catalog.prompt()` genera el system prompt, y el output es un spec plano (`root` + `elements`) validable. Tiene expresiones `$state`, `$cond`, `$template` y `$computed`, visibilidad condicional y acciones.
- **Render parcial en streaming** con `createSpecStreamCompiler`: la UI se va armando mientras el LLM responde.
- **Renderers para casi todo**: React, Vue 3, Svelte 5, Solid, React Native, Next.js, TanStack Start, Remotion (video), react-pdf, react-email, Ink (TUI), imagen SVG/PNG con Satori y React Three Fiber.
- **Catálogo listo**: `@json-render/shadcn` con 36 componentes, adapters para redux, zustand, jotai y xstate, y `@json-render/mcp` para MCP Apps en Claude, ChatGPT, Cursor y VS Code.
- **Adopción grande**: 18.1k stars y ~5,3M descargas mensuales de `@json-render/core` en npm. v0.21.0 (18-sep-2026).
- Tiene una composición experimental con [[jev]] (`experimental_composeSpec`), todavía sin release.

## Uso básico

```bash
npm install @json-render/core @json-render/react   # o @json-render/shadcn
```

**Trampas:**
- Sigue en 0.x, con 31 versiones en 8 meses: esperar breaking changes.
- Es Vercel **Labs**: experimental, no un producto GA con soporte.

Relacionado: [[fastmcp]] también arma "apps" que se renderizan dentro de la conversación, [[eve]] es el framework de agentes de Vercel, y [[kombai]] genera código de frontend en vez de specs. En el canal se lo marcó como referencia para mold.

**Licencia**: Apache-2.0
