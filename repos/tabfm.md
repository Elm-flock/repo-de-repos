---
title: tabfm
url: https://github.com/google-research/tabfm
tags: [tabular, open-weights, inference, python, google, apache-2.0]
added: 2026-08-21
added_by: Emiliano
---

Foundation model de Google Research para datos tabulares: hace clasificación y regresión **zero-shot** por in-context learning, con API compatible scikit-learn (`TabFMClassifier` / `TabFMRegressor`).

## Por qué vale la pena

- **Zero-shot sobre tablas**: no entrenás un modelo por dataset. Le pasás las filas de entrenamiento como contexto y predice — el equivalente de ICL pero para tabular.
- **Drop-in en un pipeline existente**: la API imita scikit-learn, así que reemplazar un `GradientBoostingClassifier` es cuestión de cambiar la clase.
- **Arquitectura**: atención alternada fila/columna alimentando un transformer causal de **24 bloques** con embedding dim 256. Combina la atención row/column estilo TabPFN con el ICL estilo TabICL.
- **Entrenado con cientos de millones de datasets sintéticos** generados desde modelos causales estructurales, lo que explica que generalice sin fine-tuning.
- Pesos abiertos en `google/tabfm-1.0.0-pytorch` (también hay variante JAX/Flax), release v1.0.0, ~2.5k stars. Backends JAX y PyTorch shipeados.
- Evaluado en **51 datasets de TabArena** (38 clasificación, 13 regresión).

## Uso básico

```bash
pip install "tabfm[pytorch]"   # Python >= 3.11
```

Stack pineado: JAX 0.10.1 / Flax 0.12.7 / PyTorch 2.12.1.

**Límites duros**: máximo **10 clases de salida**, optimizado para tablas de hasta **500 features**, y la memoria escala con la cantidad de filas de entrenamiento porque **todas van al contexto**. No sirve para tablas enormes.

**Licencia dual y crítica para uso en cliente**: el código es Apache-2.0, pero los **pesos están bajo "TabFM Non-Commercial License v1.0"** — no se pueden usar en producción comercial. Verificar antes de meterlo en un proyecto pago.

**Licencia**: código Apache-2.0; pesos TabFM Non-Commercial v1.0 (uso no comercial)
