---
title: kimi-k3-in-c
url: https://github.com/FareedKhan-dev/kimi-k3-in-c
tags: [llm, inference, moe, cpu, c, apache-2.0]
added: 2026-08-12
added_by: Denis
---

Motor de inferencia C99 portable para **Kimi K3** (2.78T params): corre en una sola CPU sin BLAS, sin framework y sin GPU. Peak RSS medido **8.24 GB** con checkpoint de **1.56 TB** en disco. Relacionado con [kimi-k3](kimi-k3.md) (pesos) y en la misma línea de ideas que [colibri](colibri.md) (MoE streameado desde disco).

## Por qué vale la pena

- **Misma respuesta en 8–224 GB**: output byte-identical entre presets; más RAM solo baja el reloj (laptop 8 GB ~26.5 s/tok → workstation 128 GB+ ~5.6 s/tok en sus benches).
- **Engine mínimo**: ~176 KB de código; experts 4-bit streameados desde NVMe, trunk denso residente hasta el presupuesto que elijas.
- **Cero deps de runtime**: C99 + CMake/Make; no PyTorch/llama.cpp/BLAS. Motor `./bin/k3` con presets (`laptop`, `server`, etc.).
- **Honestidad de performance**: es usable como demo/research, no como chat interactivo en laptop — ~30 s/token en 8 GB es el piso real documentado.
- **Base model**: sin chat template; continuaciones, no diálogos. Pesos del modelo original de Moonshot siguen bajo su licencia.

## Uso básico

```bash
git clone https://github.com/FareedKhan-dev/kimi-k3-in-c
cd kimi-k3-in-c && make   # o cmake; verify sin modelo en ~1 min
./bin/k3 ~/k3model --trunk ~/k3trunk --preset laptop \
  --tok ~/k3model --prompt "The capital of France is" --gen 8 --incremental
```

Requiere el checkpoint convertido (~1.56 TB en disco) y NVMe razonable. Detalle de setup en el README / `docs/`.

**Licencia**: Apache 2.0 (código; pesos Kimi K3 aparte)
