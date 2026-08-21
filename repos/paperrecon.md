---
title: paperrecon
url: https://github.com/Agent4Science-UTokyo/PaperRecon
tags: [benchmark, agents, coding-agent, python, apache-2.0]
added: 2026-08-21
added_by: Denis
---

Framework de evaluación de la Universidad de Tokio para medir calidad y riesgo de papers escritos por coding agents: el agente reconstruye un paper completo a partir de un overview y recursos mínimos (figuras, tablas, referencias, código), y el resultado se compara contra el paper real.

## Por qué vale la pena

- **Mide dos ejes ortogonales en vez de un score único**: **Presentación** (rúbrica de 1 a 5 por sección) y **Alucinación** (análisis agéntico de claims en dos etapas, grounded en el paper original), más precisión de citas como **F1**.
- **Hallazgo central e incómodo**: hay **trade-off entre calidad de presentación y tasa de alucinación** — los papers mejor presentados no son los más factuales. Es un resultado que se traslada a cualquier uso de agentes para generar documentación.
- **Benchmark PaperWrite-Bench: 51 papers** de 9 venues top, todos publicados **después de 2025** (para evitar contaminación de entrenamiento). Composición: 32 method / 12 benchmark / 7 hybrid.
- **Evalúa los agentes que usa el equipo**: Claude Code (Sonnet 4 y Sonnet 4.6) y Codex (GPT-5 y GPT-5.4).
- Artefactos públicos: repo Apache-2.0 y dataset en HuggingFace `hal-utokyo/PaperWrite-Bench`. Paper: arXiv 2604.01128, submitido el 01-abr-2026.

## Uso básico

Repo en Python del lab Agent4Science (UTokyo), ~22 stars.

**Nota sobre licencias**: el código es Apache-2.0, pero el dataset **no es permisivo de forma uniforme** — el README aclara que los papers, el LaTeX y los codebases siguen siendo propiedad intelectual de sus autores originales.

Discrepancia menor entre fuentes: la home lista los venues como ACL, CVPR, ICCV, ICLR, NeurIPS, NAACL, ACMMM y el README como NeurIPS, ICML, ICLR, CVPR, ECCV, ACL, NAACL. El conteo de 51 papers / 9 venues sí es consistente.

Relacionado: [[graph-engineer]] para el lado de estructurar contexto que estos evals terminan midiendo.

**Licencia**: Apache-2.0 (el dataset conserva la propiedad intelectual de los autores originales)
