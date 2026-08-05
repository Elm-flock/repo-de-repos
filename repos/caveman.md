---
title: caveman
url: https://github.com/JuliusBrussee/caveman
tags: [skill, claude-code, coding-agent, llm, mit]
added: 2026-08-05
added_by: Denis
---

Skill/plugin multi-agent que hace que el asistente responda en "caveman-speak": misma sustancia técnica, mucho menos relleno. Ahorra tokens de **output** (no de input). Código, comandos y errores quedan byte-a-byte.

## Por qué vale la pena

- **Números honestos**: ~65% menos output en prosa chat (10 prompts, API Claude); ~8.5% en runs agentic (JetBrains, 86 tasks SkillsBench). Calidad indistinguible en grading automático.
- **Instalador único para 30+ agents**: Claude Code, Codex, Gemini, Cursor, Windsurf, Cline, Copilot, OpenClaw, etc. Un `install.sh`/`install.ps1` detecta qué tenés.
- **Niveles**: lite / full (default) / ultra / wenyan; sticky por sesión con `/caveman <level>`. Comprime estilo, no traduce (salvo wenyan).
- **Más que el tono**: `/caveman-commit`, `/caveman-review`, `/caveman-stats`, `/caveman-compress` (memoria ~46% más chica en sesiones futuras), MCP `caveman-shrink`, subagents cavecrew-\*.
- **Ecosistema hermano**: [caveman-code](https://github.com/JuliusBrussee/caveman-code) (agent completo), cavemem, cavekit, fine-tune Gemma. Sin telemetría post-install.
- **Límite claro**: no toca input/reasoning; el skill suma ~1–1.5k input/turn. En workloads ya terse puede ser net-negative; el win fuerte es prosa/reviews/docs.

## Uso básico

```bash
curl -fsSL https://raw.githubusercontent.com/JuliusBrussee/caveman/main/install.sh | bash
# Windows: irm https://raw.githubusercontent.com/JuliusBrussee/caveman/main/install.ps1 | iex
# Un agent: npx skills add JuliusBrussee/caveman -a cursor
```

Activar con `/caveman` o "talk like caveman"; off con "normal mode". En Claude Code / Codex / Gemini suele venir on desde el primer mensaje. Node ≥18.

**Licencia**: MIT
