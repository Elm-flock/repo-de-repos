---
title: engram
url: https://github.com/Gentleman-Programming/engram
tags: [memory, mcp, coding-agent, cli, go, mit]
added: 2026-08-21
added_by: Denis
---

Sistema de memoria persistente para agentes de coding: un binario único (SQLite + FTS5) expuesto por MCP stdio, CLI, API HTTP y TUI, para que el agente recuerde decisiones entre sesiones.

## Por qué vale la pena

- **Cero dependencias de runtime**: "no Node.js, no Python, no Docker". Un binario Go y un archivo SQLite en `~/.engram/engram.db`.
- **20 tools MCP**: `mem_save`, `mem_search`, `mem_context`, `mem_timeline`, `mem_judge`, `mem_compare`, `mem_review`, `mem_doctor`, entre otras. No es sólo un key-value con búsqueda.
- **13 agentes soportados** con setup de una línea: Claude Code, Pi, OpenCode, Gemini CLI, Codex, Antigravity CLI, Windsurf, Qwen Code, Kiro, Cursor, VS Code Copilot, Kilo Code y cualquier cliente MCP.
- 6k stars, v1.20.0 (20-jul-2026), 25 contributors. Autor: Alan Buscaglia (Gentleman Programming), el mismo de [[gentle-ai]] y [[sdd-builder]] — Engram es parte explícita de ese ecosistema.
- Sync opcional entre máquinas con Postgres y dashboard web.

## Uso básico

```bash
brew install gentleman-programming/tap/engram
engram setup opencode        # o: claude-code, gemini-cli, codex, cursor, windsurf, pi...
```

En Windows conviene `go install github.com/Gentleman-Programming/engram/cmd/engram@latest`.

**Respuesta a la duda que surgió en el canal ("¿usan la cloud?")**: la "cloud" **no es un servicio hosteado**. Es un runtime que corrés vos (`engram cloud serve` + Docker + Postgres, imagen en GHCR, sólo linux/amd64 y arm64). No hay SaaS gestionado, así que la única opción es hostearla.

**Trampas concretas antes de adoptarlo:**
- El transporte MCP es **sólo stdio**: un agente dockerizado o remoto no se puede conectar por MCP.
- `engram serve` bindea **sólo a `127.0.0.1`** y no hay flag para cambiarlo, así que desde un contenedor no lo alcanzás.
- La auth del HTTP local (`ENGRAM_HTTP_TOKEN`) viene **sin setear, o sea abierto**.
- En macOS, `brew upgrade engram` mata silenciosamente un `engram serve` corriendo y el autosync se detiene.
- 188 issues abiertos en un repo de 6 meses que se mueve rápido; las features de conflictos y el export a Obsidian están marcados Beta.

**Licencia**: MIT
