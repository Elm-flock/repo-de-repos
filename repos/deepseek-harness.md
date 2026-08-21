---
title: deepseek-harness
url: https://github.com/deepseek-ai/deepseek-harness
tags: [coding-agent, cli, agents, typescript, deepseek, mit]
added: 2026-08-21
added_by: Emiliano
---

Harness de agente/coding open source de DeepSeek (`dsh`), construido sobre Cordis, donde **todo es plugin**: la UI de chat, los tool calls, la inyección de contexto e incluso el loop del agente son intercambiables.

## Por qué vale la pena

- **Plugin-everything de verdad**: el propio agent loop es un plugin. Sirve para experimentar con estrategias de loop sin forkear el harness.
- **Model-agnostic**: providers pluggables (API de DeepSeek, OpenRouter, otros). No te ata al modelo del vendor que lo publicó.
- **Adopción explosiva**: repo creado el 13-ago-2026 y ya con ~179k stars y ~19.5k forks. Vale seguirlo aunque no lo adoptes hoy.
- Toolchain estándar de TypeScript: pnpm + Vitest, así que forkear y testear es directo.

## Uso básico

```bash
npx @deepseek-ai/dsh web   # Web UI en http://127.0.0.1:3080
```

**Está en developer preview**: las 9 versiones publicadas en npm son `-rc` (última `0.1.1-rc.1`) y el README avisa en mayúsculas que habrá cambios que rompan compatibilidad. Los issues están deshabilitados — el soporte va por Discussions y Discord.

Nota menor: el manifest de npm de la versión `0.0.1-rc.1` declara BSD-3-Clause, pero el `LICENSE` del repo y el SPDX de GitHub dicen MIT.

Relacionado: [[openharness]], [[herdr]] y [[codewhale]] como otros harnesses/CLIs de agentes.

**Licencia**: MIT
