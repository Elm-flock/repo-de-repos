---
title: hallmark
url: https://github.com/nutlope/hallmark
tags: [coding-agent, claude-code, skill, design, mit]
added: 2026-07-30
added_by: Emiliano
---

"Design skill" para asistentes de coding con IA que genera y audita UI web rechazando los defaults genéricos de LLM ("anti-AI-slop"). No es una librería ni un modelo: es un rule-set + prompts empaquetados como skill instalable. Hecho por Together AI (Nutlope / Hassan El Mghari).

## Por qué vale la pena

- **Multi-herramienta**: instalable en Claude Code (`~/.claude/skills/hallmark/`), Cursor (`.cursor/rules/hallmark.mdc`) y Codex (`~/.codex/skills/`).
- **20 temas + 57 "slop-test gates"** que corre antes de devolver código, más un self-critique pre-emisión.
- **Cuatro comandos**: `build` (default), `audit <target>` (puntúa código existente contra anti-patrones), `redesign <target>` (reconstruye estructura conservando copy/brand), `study <screenshot|URL>` (extrae "design DNA", opcionalmente emite un `design.md` portable).
- **Codifica el "anti-slop consensus"**: tipografía, color, layout, motion, microinteracciones y variedad estructural en un rule-set opinado; rechaza los defaults on-distribution en los que todo LLM fue entrenado.
- Tracción alta (~20k estrellas, crecimiento rápido en 2026). Hay forks/copias: el canónico es `nutlope/hallmark`.

## Uso básico

```bash
npx skills add nutlope/hallmark
```

**Licencia**: MIT
