---
title: opendots
url: https://github.com/CopilotKit/OpenDots
tags: [agents, multi-agent, self-hosted, typescript, mit]
added: 2026-10-09
added_by: Emiliano
---

Template de CopilotKit para montar "coworkers" de IA persistentes ("Dots"): cada uno tiene rol, permisos y su propia computadora (browser, archivos y shell en contenedor), y se habla con ellos por chat, llamada de voz o Slack. El trabajo queda como páginas editables en "Spaces". **El código es MIT, pero las conversaciones requieren CopilotKit Intelligence, que es propietario.** Está en alpha y tiene dos semanas.

## Por qué vale la pena

- **Cada agente con su computadora**: los contenedores salen de `CopilotKit/OpenBot` (MIT, 6,2k stars). Las herramientas MCP por Dot que no son read-only piden aprobación humana.
- **Stack abierto y conocido**: CopilotKit 1.75 con AG-UI (el protocolo que publica CopilotKit), `@tanstack/ai` contra cualquier proveedor compatible con OpenAI, React 19, TipTap y SQLite.
- **Estado declarado sin maquillaje**: probado con servicios reales en chat, Spaces, Dot computers y llamadas; sólo en local los specialist Dots y el trabajo programado; sin probar en vivo la delegación por voz y Slack.
- 4,6k stars en 10 días.

## Uso básico

```bash
git clone https://github.com/CopilotKit/OpenDots.git && cd OpenDots
npm ci && cp .env.example .env    # completar OPENAI_API_KEY y OPENAI_MODEL
npx copilotkit@latest login && npx copilotkit@latest project select
npm run dev                       # http://127.0.0.1:5173
```

Requiere Node 24.

**Trampas:**
- **Intelligence tiene tres formas, ninguna libre**: el servicio hosteado (mensajes, tool calls y eventos van a la nube de CopilotKit); un "local evaluation preview" en Docker Desktop, sólo macOS, 12 GiB de RAM, 30 días renovables y "not a production installation"; o self-hosted con licencia paga. Sin Intelligence sólo funcionan las páginas y la config.
- Single-owner: no hay edición compartida, invitaciones, uploads ni grupos multi-Dot.
- Telemetría activada por defecto (`COPILOTKIT_TELEMETRY_DISABLED=true` o `DO_NOT_TRACK=1`). La búsqueda web va por defecto a Parallel.

Otras bases para armar plataformas de agentes: [[eve]] y [[openharness]].

**Licencia**: MIT el template; CopilotKit Intelligence es propietario
