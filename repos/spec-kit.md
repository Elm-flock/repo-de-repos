---
title: spec-kit
url: https://github.com/github/spec-kit
tags: [spec-driven, coding-agent, cli, python, github, mit]
added: 2026-08-21
added_by: Emiliano
---

Toolkit de GitHub que instala un pipeline de spec-driven development (constitution → spec → plan → tasks → implement) como slash commands dentro del agente de coding que ya usás.

## Por qué vale la pena

- **130.6k stars**, ~268 contributors, y **llegó a v1.0.0 el 21-ago-2026**, justo un año después de crearse el repo. Es el más adoptado del rubro por lejos: [[openspec]] tiene 65.8k, la mitad.
- **40 integraciones de agente** (el README se subestima diciendo "30+"), y 15 soportan modo skills en vez de archivos de slash command: Claude Code, Codex, Copilot CLI, Cursor, Gemini, opencode, Devin, Kiro, Qwen, Antigravity.
- **Resolución de templates en 4 capas**: overrides del proyecto > presets > extensions > core. Más un sistema de bundles con catálogo priorizado (proyecto > usuario > built-in) y políticas `install-allowed` vs `discovery-only`.
- **Scripts duales Bash + PowerShell**, así que el soporte de Windows es nativo y no vía WSL.
- Comandos: `/speckit.constitution`, `.specify`, `.plan`, `.tasks`, `.taskstoissues`, `.implement`, `.converge`, más `.clarify`, `.analyze` y `.checklist` opcionales.
- Ritmo alto: 7 releases en 17 días antes del 1.0.

## Uso básico

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@v1.0.0
specify init my-project --integration copilot
```

**Trampa concreta**: **PyPI va atrasado respecto de GitHub.** `specify-cli` en PyPI todavía está en **0.16.5** (19-ago), así que `uv tool install specify-cli` te trae 0.16.5, no la 1.0.0. Para la 1.0.0 hay que usar la forma con git ref.

**Y el 1.0.0 no significa API estable.** Las release notes lo dicen explícitamente: el seguro que vende un 1.0.0 es contra un costo "que en gran medida se derrumbó", y describen el versionado más como una ola que como un congelamiento. No lo leas como garantía de compatibilidad.

Otras cosas: `specify init` interactivo se cuelga en CI o en PTYs de agentes (usar `--non-interactive`), y las extensions de la comunidad son código de terceros que se escribe en los directorios de tu agente al instalar — el README pide revisarlas antes.

**Sobre la comparación que surgió en el canal** ("Spec kit me gastó mucho más, pero también creo que tiene más estructura"): **no existe ningún benchmark publicado de consumo de tokens contra OpenSpec.** La percepción es consistente con su estructura — 10 comandos, templates grandes, un artefacto de constitution y pasadas de `analyze`/`checklist` cruzando artefactos — pero es percepción, no dato medido.

Relacionado: [[openspec]], [[sdd-builder]], [[kdd]] y [[bmad-method]] como el resto del rubro.

**Licencia**: MIT
