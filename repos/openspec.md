---
title: openspec
url: https://github.com/Fission-AI/OpenSpec
tags: [coding-agent, spec-driven, cli, mcp, mit]
added: 2026-07-30
added_by: Emiliano
---

Framework/CLI de spec-driven development (SDD) para asistentes de IA de código. Alinea a humanos y agentes sobre qué construir *antes* de escribir código, usando specs y "changes" en Markdown plano. Mantenido por el equipo Fission-AI.

## Por qué vale la pena

- **Tool-agnostic**: funciona con 30+ herramientas (Claude Code, Cursor, Copilot, OpenCode, etc.).
- **Specs en Markdown plano** con escenarios concretos, sin sintaxis propietaria.
- **Filosofía "fluid not rigid / iterative not waterfall"**: sin phase-gates rígidos.
- **Brownfield-ready**: pensado para adoptar en proyectos existentes, no solo greenfield.
- **Feature beta "Stores"**: planificación compartida cross-repo para equipos.

## Uso básico

```bash
npx openspec init
# luego se opera vía slash-commands del asistente de código
```

**Licencia**: MIT
