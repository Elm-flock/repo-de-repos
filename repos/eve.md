---
title: eve
url: https://github.com/vercel/eve
tags: [agents, framework, typescript, vercel, apache-2.0]
added: 2026-08-10
added_by: Francisco
---

Framework de Vercel para agentes durables donde **el filesystem es la interfaz de autoría**: las capacidades del agente viven en ubicaciones convencionales del repo, así que el proyecto se inspecciona, extiende y opera como código normal. Instrucciones y skills en Markdown, tools en TypeScript.

## Por qué vale la pena

- **Layout convencional en vez de configuración**: `agent/instructions.md` (system prompt siempre activo, lo único requerido), `agent/tools/*.ts` (funciones tipadas), `agent/skills/*.md` (procedimientos cargados on demand), `agent/channels/*.ts` (HTTP, Slack, Discord), `agent/schedules/*.ts` (cron), `agent/agent.ts` (modelo y runtime).
- **Durable por defecto**: los agentes sobreviven al request, con human-in-the-loop, subagentes y schedules como primitivas del framework.
- **Tools tipadas con Zod** vía `defineTool`, y elección de modelo declarativa en `defineAgent`.
- **El paquete npm trae su documentación adentro** (`node_modules/eve/docs`), pensado para que un coding agent la lea local sin salir a la web.
- Canales de mensajería y schedules ya resueltos — es la parte que normalmente te toca cablear a mano.

## Uso básico

```bash
npx eve@latest init my-agent   # scaffold + deps + git + TUI interactiva
# o sobre un proyecto existente:
npx eve@latest init .
npm run dev
```

Está en **beta** bajo los beta terms de Vercel: framework, APIs, docs y comportamiento pueden cambiar antes de GA.

**Licencia**: Apache 2.0
