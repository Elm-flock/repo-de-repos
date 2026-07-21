---
title: codewhale
url: https://github.com/Hmbown/CodeWhale
tags: [llm, cli, coding-agent, rust, hmbown, mit]
added: 2026-07-21
added_by: Emiliano
---

Agente de código local escrito en Rust, con TUI y modo headless, que permite usar modelos hospedados o locales desde un mismo runtime.

## Por qué vale la pena

- **Sin lock-in de modelo**: integra DeepSeek, Claude, GPT, Kimi, GLM y más de 30 proveedores, además de vLLM, SGLang y Ollama locales.
- **Controles de riesgo reales**: combina modo Plan de sólo lectura, aprobaciones, hooks y sandboxing nativo con Seatbelt en macOS o Landlock, seccomp y bwrap en Linux.
- **Reglas que el agente no puede saltear**: las invariantes de `.codewhale/constitution.json` se convierten en bloqueos de escritura incluso en Full Access.
- **Trabajo durable**: Fleet ejecuta varios workers y registra los pasos en un ledger append-only que se puede retomar después de un reinicio.
- **Integración amplia**: habla MCP en ambas direcciones, carga skills, expone APIs HTTP/SSE y ACP, y cuenta con una GUI comunitaria para VS Code.
- **Migración preservada**: nació como `deepseek-tui`; la configuración y las sesiones existentes se conservan al pasar a CodeWhale.

## Uso básico

```bash
npm install -g codewhale
codewhale auth set --provider deepseek
codewhale
codewhale exec "fix the failing test"
```

También ofrece instalaciones por Cargo, Docker, Nix, Scoop, binarios precompilados y Termux.

**Licencia**: MIT
