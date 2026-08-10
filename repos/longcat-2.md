---
title: longcat-2
url: https://longcatai.org/models/longcat-2
tags: [llm, moe, coding-agent, agents, open-weights]
added: 2026-08-10
added_by: Emiliano
---

LLM MoE de 1.6T parámetros orientado a agentic coding, con contexto nativo de 1M tokens y pesos abiertos. El diferencial es la activación dinámica: 33B–56B params por token (~48B promedio) según la dificultad del token, no un ancho fijo.

## Por qué vale la pena

- **Benchmarks agénticos fuertes**: SWE-bench Pro 59.5, SWE-bench Multilingual 77.3, Terminal-Bench 2.1 70.8, BrowseComp 79.9.
- **LongCat Sparse Attention**: baja la complejidad de cuadrática a lineal, que es lo que hace viable el contexto de 1M nativo (no extendido a posteriori).
- **Zero-Computation Experts + ScMoE**: asignación de recursos a nivel token — los tokens fáciles gastan menos cómputo.
- **Entrenado con 30T+ tokens** (chino, inglés, multilingüe y código) sobre un cluster doméstico de 50.000 placas, refinado con MOPD (Multi-Teacher On-Policy Distillation) combinando grupos de expertos de Agent, Reasoning e Interaction.
- **Escala accesible sin ser frontier-cerrado**: a ~48B activos, el costo de inferencia es mucho menor que el que sugiere el 1.6T total.

## Uso básico

Disponible vía longcat.ai y OpenRouter. Los pesos se publican en Hugging Face / GitHub.

Igual que con kimi-k3: 1.6T totales es infra de datacenter multi-GPU, no una workstation.

**Licencia**: open source según el propio anuncio — verificar los términos exactos al descargar los pesos.
