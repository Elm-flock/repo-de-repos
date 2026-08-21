---
title: vord
url: https://github.com/pmaojo/vord
tags: [security, sast, coding-agent, mcp, rust, mit]
added: 2026-08-21
added_by: Emiliano
---

Plataforma de análisis estático en Rust que actúa como guardrail en tiempo de escritura: juzga el write de un agente **antes de que llegue al disco**, vía hooks del editor o del agente. Trae además su propio agente de coding, juzgado por ese mismo gate.

## Por qué vale la pena

- **Gatea el write, no el commit**: `vord hook check` sale con 0, o 2 si deniega. Es un punto de control bastante más temprano que un pre-commit o un CI.
- **Publica sus números malos**, que es lo que le da credibilidad: en OWASP Benchmark v1.2 (2.740 casos, 253k LOC) reporta **precisión 52.79%, recall 70.11%, F1 60.23% y una tasa de falsos positivos de 66.94%**, con la categoría `cmdi` en 17.46% de recall. Sabés a qué te expones.
- **Volumen real**: 16 crates core, 8 de infra, **24 parsers de lenguaje**, 18 crates de rulesets (`owasp`, `code-smells`, `architecture`, `ddd`, `a11y`, `secrets`, `iac`, `ai-agent`…), 614 archivos `.rs`. Dirección de dependencias forzada por Cargo.
- **Agent Permission Policy** (`vord-policy.toml`) con circuit breaker y loop guard — pensado para cuando el agente entra en loop.
- **Empaquetado de cuatro formas**: GitHub Action, plugin de Claude Code (`vord-guardrail`), paquete Agent Plugins Spec v1.0.0 y bridge para [[deepseek-harness]].
- Releases con 16 assets cada uno: binarios de CLI y LSP para 4 targets con `.sha256`. v0.14.0 del 20-ago-2026, 26 releases en 30 días.

## Uso básico

```bash
curl -fsSL https://raw.githubusercontent.com/pmaojo/vord/main/scripts/install.sh | sh
vord scan .
vord hook install     # escribe .claude/settings.json y vord-policy.toml
```

**Tres de los cinco canales de instalación que documenta el README no existen** — verificado contra los registries:
- `cargo install vord-cli` **falla**: no hay nada en crates.io, a pesar de que el README afirma que el workspace publica ahí.
- `npx vord scan .` **falla**: no hay paquete `vord` en npm.
- `brew install pmaojo/tap/vord` **falla**: el tap da 404.
- `uses: pmaojo/vord@v0` **falla**: no existe el tag `v0`. Con `@main` o `@v0.14.0` sí anda.

**Otras cosas a saber:**
- **2 stars, 0 forks, 0 descargas en todos los assets de v0.14.0.** El README es muchísimo más grande que la adopción.
- Version desync: `Cargo.toml` en `main` dice 0.13.4 y el último release es v0.14.0.
- El autor aclara que no hay type checker ni borrow checker: código que pasa todas las reglas puede igual no compilar.
- La capa hosteada (`vord-cloud`) es un repo privado aparte.
- Tiene committeado en la raíz un `info.md` de 57 KB que es un transcript crudo de LLM en español ("¡Perfecto! Aquí tienes la versión ampliada...") — en un repo que vende higiene de código.

**Nota**: el artículo de LinkedIn con el que llegó al canal ("por qué deberías dejar de leer el código que genera la IA") no es sobre vord. Esa tesis viene de `AmazingAng/old-coder`, que vord vendorea literalmente en `skills/old-coder/SKILL.md`; vord implementa el paso GAUNTLET de ese loop.

Relacionado: [[visa-vulnerability-agentic-harness]] y [[agent-governance-toolkit]] para las otras capas del mismo problema.

**Licencia**: MIT
