---
title: herdr
url: https://github.com/herdrdev/herdr
tags: [cli, coding-agent, multi-agent, rust, apache-2.0]
added: 2026-07-30
added_by: Emiliano
---

Multiplexer de terminal "agent-aware" (estilo tmux) para correr varios CLIs de agentes de IA en paneles reales simultáneos, con detección automática del estado de cada agente. Un solo binario en Rust, sin Electron ni dependencias externas. Se describe como "the runtime your coding agents live on".

## Por qué vale la pena

- **Detección de estado por agente** en un sidebar (idle / working / blocked / done), lo que lo distingue de tmux/zellij genéricos.
- **Auto-detección de agentes**: Claude Code, Codex, OpenCode, Grok CLI, Cursor Agent, GitHub Copilot CLI, Droid, Amp… y cualquier agente de terminal funciona out of the box.
- **Sesiones persistentes** tipo tmux: sobreviven a desconexiones del cliente; detach/reattach incluso por SSH y desde el celular.
- **Workspaces con tabs y panes anidados**: prefijo `ctrl+b`, soporte de mouse (click/drag/split); cada pane renderiza el terminal real, así que ANSI/TUI se ven correctamente.
- **Un único binario Rust**; ~22k estrellas; versión v0.4.0; llegó al #1 de GitHub Trending (30-jun-2026).

> Nota: el repo se movió de `ogulcancelik/herdr` a `herdrdev/herdr` (mismo autor). Varios blogs dicen AGPL-3.0, pero el LICENSE oficial actual es Apache-2.0, sin dual-licensing.

## Uso básico

```bash
curl -fsSL https://herdr.dev/install.sh | sh
# alternativas: brew install herdr  ·  mise use -g herdr
```

**Licencia**: Apache 2.0
