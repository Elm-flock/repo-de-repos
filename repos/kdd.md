---
title: kdd
url: https://github.com/MauricioPerera/KDD
tags: [spec-driven, coding-agent, agents, python, mcp, mit]
added: 2026-08-21
added_by: Emiliano
---

Template repository + metodología para gobernar agentes de coding efímeros con gates determinísticos y **sin LLM juzgando**: conocimiento como nodos markdown enlazados, más contratos por tarea con hashes de test congelados.

## Por qué vale la pena

- **Gates determinísticos, no un modelo opinando**: ~40 scripts de validación en Python, todos stdlib, sin LLM y sin red. `validate_contracts.py`, `validate_okf.py`, `audit_forbids.py`, `assemble_context.py`, `export_gate_contract.py`, entre otros. Es la diferencia con los enfoques donde un LLM decide si el LLM hizo bien.
- **19 gates** derivados del dispatch de MCP en vez de hardcodeados, con `preflight.py` para correrlos todos en dry-run local antes de tocar CI.
- **~30 módulos de test** (~380 KB) para las propias herramientas. El validador está testeado.
- **Dos modos de distribución para CI**: un reusable workflow con 17 inputs y una composite action que copia el tooling a `_kdd/`, así un repo que no es fork puede correr los gates.
- **Wiring para 5 ecosistemas de agentes** desde una sola fuente (`.agents/AGENTS.md`), con punteros finos en `.cursorrules`, `.clinerules`, `.windsurfrules`, `copilot-instructions.md` y `CLAUDE.md`. Más 9 agent skills (`kdd-security-scan`, `kdd-privacy-scan`, `kdd-accessibility-scan`, `kdd-test-coverage-scan`, `kdd-dependency-eol-scan`…).
- 33 contratos de ejecución con su reporte verificado, 7 JSON Schemas y un MCP server. v1.12.0 (26-jul-2026), 13 releases en 19 días.

## Uso básico

```bash
git clone <tu-fork> mi-proyecto && cd mi-proyecto
python scripts/init_project.py --apply --name "Mi Proyecto"   # limpia los artefactos de ejemplo
python scripts/preflight.py --agent                            # dry-run de los 19 gates
```

**Cosas a tener en cuenta:**
- **4 stars, 3 forks.** Adopción prácticamente nula frente a lo elaborado que es. Último push 31-jul-2026 (~3 semanas).
- **Docs y comentarios mayormente en español y forzados a ASCII** (`lint_ascii.py` es un gate), así que el texto aparece sin acentos: "indireccion", "codigos". El README es trilingüe, pero la base de conocimiento profunda es sólo español — incluido un `casos-reales.md` de 171 KB.
- **El "OKF" de KDD no es el [[okf]] de Google, y son incompatibles.** El de acá exige 4 claves de frontmatter, restringe `type` a exactamente 4 valores ("cualquier otro valor es inválido") y obliga a que todo nodo esté enlazado desde `index.md`. El de Google pide sólo `type`, rechaza explícitamente una taxonomía fija y prohíbe al consumidor rechazar tipos desconocidos. Un bundle de uno falla el validador del otro.
- El LICENSE dice `Copyright (c) 2026` **sin nombrar titular**.
- Vendorea `openai/codex-security` bajo `scripts/vendor/`.

Llegó al canal junto con [[okf]] ("de la mano del okf, sale el kdd"). Comparar con [[openspec]], [[sdd-builder]] y [[gentle-ai]] como enfoques vecinos de spec-driven.

**Licencia**: MIT
