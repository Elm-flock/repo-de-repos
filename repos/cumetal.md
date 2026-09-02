---
title: cumetal
url: https://github.com/Lulzx/cuda-metal
tags: [gpu, cuda, metal, cpp, apache-2.0]
added: 2026-09-02
added_by: Denis
---

Recompila un subconjunto testeado de CUDA C++ y PTX a Metal, con un runtime clean-room de compatibilidad CUDA para Apple Silicon. El equivalente de [[zluda]] pero apuntando a Metal en vez de a AMD.

## Por qué vale la pena

- **Pipeline de compilación real, no un wrapper**: Clang/NVVM → CuMetal IR → MSL → metallib.
- **Pasa el gate headless de `cuda-samples` de NVIDIA: 83/83, cero waivers** (rerun del 30-ago-2026). El denominador funcional propio da 185/185 sin skips en un M4 Pro.
- **Corpus de 27 proyectos con ejecución numérica verificada en GPU Apple**, más una demo de GROMACS que gana en `ns/day` contra Metal nativo y contra el backend Metal de AdaptiveCpp en workloads de agua acotados.
- **Ritmo sostenido**: creado 18-feb-2026, 8 releases, la v0.4.0 del 31-ago-2026. Llegó a Show HN el 25-ago-2026.
- El README es inusualmente honesto sobre lo que no funciona, lo cual lo hace más confiable que el promedio.

## Uso básico

```bash
brew install lulzx/tap/cumetal && cumetal doctor
# o desde fuente
cmake -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j"$(sysctl -n hw.ncpu)"
build/cumetalc samples/vectorAdd/vectorAdd.cu -o vectorAdd && ./vectorAdd
build/cumetalc kernel.cu --emit=cumetal-ir|msl|metallib -o kernel.X
```

Requiere macOS 14+ en Apple Silicon, CMake, LLVM 18+, un frontend Clang 21-23 con soporte CUDA y las herramientas `metal`/`metallib` de Apple.

**Lo que hay que saber antes de contar con esto**:

- Se autodeclara **experimental**, y **no es un drop-in de NVIDIA**: "las APIs de CUDA y de las librerías son subconjuntos testeados". Los paths no soportados fallan explícitamente en vez de dar resultados dudosos, lo cual es lo correcto pero significa que hay que probar tu código.
- **FP64 no es nativo**: se emula por software vía `fast48`, `wide48` o `ieee64`, con semánticas de precisión distintas — "esto no es FP64 nativo de Metal".
- Sin SASS, sin multi-GPU, sin peer access, sin interop con APIs gráficas. `multiProcessorCount` se reporta como 1 y la sincronización cross-threadgroup está capada en 4 bloques.
- El alias `libcuda.dylib` viene **deshabilitado en builds Release** salvo que lo actives con `-DCUMETAL_ENABLE_BINARY_SHIM=ON`.
- **2 contributors** (522 commits de `Lulzx`), 165 stars: proyecto de un autor.
- Ojo con leer de más los números: el propio README aclara que la matriz 29/29 de metallib son **resultados de compilación, no prueba numérica en runtime**.

**Alternativa**: el backend Metal de AdaptiveCpp con soporte de dialecto CUDA (PR #1983) es el competidor directo. `CUDAM` y `vkom` aparecen en búsquedas pero están abandonados (sin push desde ago-2025 y abr-2026).

**Licencia**: Apache-2.0
