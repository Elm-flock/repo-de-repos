---
title: mobiai-core
url: https://github.com/ArisGuimera/MobiAI-Core
tags: [skill, coding-agent, mobile, cli, go, mit]
added: 2026-08-21
added_by: Emiliano
---

CLI + ecosistema de agent skills que instala expertise de desarrollo mobile (Android, iOS, Flutter, React Native, KMP) dentro de un agente de coding que ya usás, más un grafo semántico de código y memoria por proyecto.

## Por qué vale la pena

- **39 archivos `SKILL.md` en 8 packs**. El pack `core` (21 skills) trae cosas concretas como `mobiai-fix-issue`, `mobiai-analyze-crash`, `mobiai-crashlytics`, `mobiai-mobile-tdd` y `mobiai-mobile-worktrees`.
- **6 de las 10 skills de Android son de autoría de Google**: `agp-9-upgrade`, `navigation-3`, `migrate-xml-views-to-jetpack-compose`, `r8-analyzer`, `edge-to-edge`, `play-billing-library-version-upgrade`. Eso es lo que lo diferencia de un set de prompts caseros.
- **Escrito en Go** con binarios precompilados para 6 targets (darwin/linux amd64+arm64, windows amd64+arm64): no arrastra Node ni Python.
- **Multi-host**: ships `.claude-plugin/`, `.cursor-plugin/`, `.codex/`, `gemini-extension.json`, más `CLAUDE.md`, `AGENTS.md` y `GEMINI.md`.
- Packs versionados aparte del CLI (`android--v2.0.0`, `ios--v2.0.0`), así que podés actualizar el conocimiento sin tocar el binario.

## Uso básico

```bash
curl -fsSL https://mobiai.dev/install.sh | sh    # macOS/Linux
mobiai doctor
mobiai skills add mobile     # meta-pack: todo
mobiai graph init            # indexa en .mobiai/graph/
```

**Estado real**: el CLI está en **0.2.3** (pre-1.0) y el último release es del 04-jun-2026, ~2.5 meses más viejo que el último commit. El autor declara CLI y Skills como Stable, pero **Graph y Brain como Alpha**, y los Agents "en desarrollo". Bus factor de 1-2 (441 stars, 2 contributors) y el install es `curl | sh` desde un dominio en Vercel.

Autor: Aris Guimerá (AristiDevs). Llegó al canal por el video "Adiós prompts genéricos: llega MobiAI para mobile".

Relacionado: [[skillsmp]], [[power-platform-skills]] y [[caveman]] como otros paquetes de skills.

**Licencia**: MIT
