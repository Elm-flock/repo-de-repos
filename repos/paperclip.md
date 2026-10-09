---
title: paperclip
url: https://github.com/paperclipai/paperclip
tags: [multi-agent, coding-agent, self-hosted, typescript, mit]
added: 2026-10-09
added_by: Guille
---

Servidor self-hosted (Node.js + UI React) que orquesta "compañías" de agentes de IA: organigrama, tareas tipo ticket, presupuestos, aprobaciones y heartbeats. No es un framework de agentes: maneja los que ya usás. **Telemetría activada por defecto, quickstart sin autenticación y breaking changes en releases regulares.**

## Por qué vale la pena

- **Maneja los agentes que ya tenés**: adapters para Claude Code, Codex, Cursor (y Cloud), Gemini CLI, [[opencode]], [[pi]], Hermes, OpenClaw, Grok Build y Kimi Code, más procesos custom y endpoints HTTP o webhook.
- **Sandboxes intercambiables**: e2b, Cloudflare, Daytona, Modal, Novita o Kubernetes self-hosted.
- **Un solo proceso** con PostgreSQL embebido y storage local; UI y API en `:3100`. En producción se apunta a un Postgres propio o se usa Docker. Trae un "native runner" en Rust.
- **Crecimiento enorme**: 99k stars y 16,7k forks en 7 meses, 2.700+ PRs mergeados. CalVer con releases cada 1-2 semanas (último `v2026.1005.0`, 6-oct-2026).
- Comunidad: `gsxdsm/awesome-paperclip` (catálogo de plugins), `NousResearch/hermes-paperclip-adapter`, `mvanhorn/paperclip-plugin-acp` (Claude Code, Codex y Gemini vía ACP) e `istib/obsidian-paperclip`.

## Uso básico

```bash
npx paperclipai@latest onboard --yes
npx paperclipai@latest onboard --yes --bind tailnet    # o --bind lan, modo autenticado
ANTHROPIC_API_KEY=... npx paperclipai test-drive
PAPERCLIP_TELEMETRY_DISABLED=1                          # o DO_NOT_TRACK=1
```

Requiere Node 24.11+ (y pnpm 9.15+ desde el código).

**Trampas:**
- El quickstart arranca en modo "trusted local loopback", sin auth. Para exponerlo, `--bind lan` o `--bind tailnet`.
- Los presupuestos se aplican sobre gasto ya reportado: el trabajo en curso puede pasarse del corte (lo avisa el README). El marketing es "empresas autónomas 24/7", así que vigilá el costo en tokens.
- Agent Chat y los conectores de memoria son experimentales. Paperclip Cloud es sólo waitlist, sin precios públicos.

Para correr varios agentes en paralelo sin la capa de "compañía": [[orca]] y [[herdr]]. Para equipos de agentes dentro de Claude Code: [[agent-teams]].

**Licencia**: MIT (Paperclip Labs, Inc.)
