---
title: bmad-method
url: https://github.com/bmad-code-org/BMAD-METHOD
tags: [spec-driven, agents, multi-agent, coding-agent, nodejs, mit]
added: 2026-08-21
added_by: Emiliano
---

"Breakthrough Method for Agile Ai Driven Development": framework agéntico que instala agentes por rol (analyst, PM, architect, dev, review) y workflows dimensionados según el tamaño de la tarea dentro de tu herramienta de coding.

## Por qué vale la pena

- **52.1k stars**, ~151 contributors, creado en abr-2025 — tiene bastante más rodaje que la mayoría del rubro. Minors mensuales sostenidos.
- **La v6.11.0 (10-ago-2026) es una consolidación con números concretos**: baja las skills core de **14 a 8** y, sobre ~560 archivos, **borra ~1.900 líneas más de las que agrega**. Es un proyecto que poda, no sólo acumula.
- **Criterios de review aritméticos, no a ojo**: el follow-up se dispara con `true si hay algún high, o si 3 × medium + 1 × low ≥ 5`. Determinístico.
- `scripts/sprint_plan.py` tiene **37 tests**.
- **Ecosistema oficial de módulos** en repos aparte, registrados en `bmad-modules.yaml`: bmad-builder, creative-intelligence-suite, test-architecture-enterprise, bmad-loop, game-dev-studio.
- **Web bundles** que empaquetan los workflows como Gemini Gems y Custom GPTs de ChatGPT, si no querés usarlo desde un CLI.
- 21k descargas semanales en npm, 493 versiones publicadas.

## Uso básico

```bash
npx bmad-method install
# después, dentro de tu agente:
bmad-build "<lo que querés cambiar>"
```

Necesita Node ≥20.12.0, **y Python 3.10+ con `uv`**: las skills renderizadas (`bmad-build`, `bmad-build-auto`) **abortan si `uv` no está**, sin fallback a otro intérprete.

**Detalle de licencia que rompe scanners**: el código es MIT, pero la API de GitHub reporta `NOASSERTION` porque el archivo LICENSE le agrega un **TRADEMARK NOTICE** — BMad™, BMad Method™ y BMad Core™ son marcas de BMad Code, LLC, "cubriendo todas las capitalizaciones y variantes (incluyendo BMAD, bmad, BMadMethod, BMAD-METHOD, etc.)". El código es libre; el nombre no.

**Migración en curso, con cosas que rompen:**
- La v6.11.0 renombra `bmad-quick-dev` → `bmad-build` y `bmad-dev-auto` → `bmad-build-auto`. Los shims redirigen pero **piden aprobación explícita y abortan en corridas desatendidas** si usás los nombres viejos con overrides `.toml` legacy.
- Los IDs deprecados viven en `v6-shims/` y **se eliminan en el corte de la v7**. Cuatro ya se fueron.
- Los renderers ahora **salen con 1** ante una config key faltante u override no parseable; antes sustituían silenciosamente por string vacío.
- El propio release lo dice: "este release es la migración, no el cutover". La config TOML por capas ya está, pero sigue existiendo `config.yaml` por módulo.

Llegó al canal como "bmat", en la comparación con [[spec-kit]] y [[openspec]] ("el que no pude probar aún").

**Licencia**: MIT, con notice de marca registrada sobre el nombre
