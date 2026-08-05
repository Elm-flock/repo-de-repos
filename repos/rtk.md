---
title: rtk
url: https://github.com/rtk-ai/rtk
tags: [cli, llm, coding-agent, rust, rtk-ai, apache-2.0]
added: 2026-08-05
added_by: Denis
---

Proxy CLI en Rust (binario único) que intercepta comandos de shell de coding agents y comprime el output antes de que entre al contexto del LLM. Corta hasta ~90% del bash output en comandos comunes; overhead <10 ms.

## Por qué vale la pena

- **Ahorro medible en la fuente correcta**: no promete −90% de la factura; reduce el output de bash (un pedazo del input). Estimación `bytes/4`, con dashboard `rtk gain`.
- **100+ comandos con filtros propios**: `ls`/`tree`, `cat`/`read`, `grep`/`rg`, git, gh, pytest/cargo/jest/go test, docker/kubectl, AWS, linters, etc. Tests suelen colapsar a failures only (−90% tipificado).
- **Hooks en muchos agents**: Claude Code, Copilot, Gemini, Codex, Cursor, Windsurf, Cline, Pi, Hermes, etc. Tras `rtk init`, `git status` se reescribe a `rtk git status` sin que el agent lo pida.
- **Cuatro estrategias por comando**: smart filtering, grouping, truncation y deduplicación; flag `--ultra-compact` para apretar más.
- **DSL y analytics**: filtros custom vía TOML, `rtk discover` para oportunidades perdidas, `rtk session` para adopción. Telemetría opt-in (off por defecto).
- **Cuidado**: otra crate `rtk` en crates.io (Rust Type Kit). Instalar desde Homebrew, `install.sh` o `cargo install --git`.

## Uso básico

```bash
brew install rtk
# o: curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh
rtk init -g                     # Claude Code / Copilot
# rtk init -g --agent cursor
rtk --version && rtk gain
```

Reiniciar el agent después del init. Los tools nativos tipo Read/Grep/Glob de Claude Code no pasan por el hook Bash; para esos, `rtk read` / `rtk grep` / `rtk find`.

**Licencia**: Apache 2.0
