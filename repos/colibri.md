---
title: colibri
url: https://github.com/JustVugg/colibri
tags: [llm, inference, moe, quantization, c, apache-2.0]
added: 2026-07-20
added_by: Emiliano
---

Motor de inferencia en C puro que permite correr GLM-5.2 (Mixture-of-Experts de 744B parámetros) en hardware de consumidor con ~25GB de RAM, streameando los pesos de los experts desde disco.

## Por qué vale la pena

- **Jerarquía de memoria unificada**: trata VRAM, RAM y storage como un solo espacio manejado; los experts viven en disco por default y ocupan VRAM/RAM según el hardware disponible — pero "el placement solo decide velocidad", nunca cambia la precisión ni las decisiones del modelo.
- **Cero dependencias en runtime**: implementación en C puro (Python solo se usa una vez, para convertir el modelo).
- **Cuantización fiel**: validada token-exact contra las implementaciones de referencia, sin cambios silenciosos de precisión.
- **Cache adaptativo**: aprende el patrón de uso y pinea automáticamente los experts más usados, mejorando con el tiempo.
- **Pipeline por token en 5 pasos**: route → union → place → overlap → learn, con I/O async, batch-union y prefetching por lookahead del router para minimizar la espera de disco.
- **Extras**: decoding especulativo (MTP head), API compatible con OpenAI, dashboard web con métricas en tiempo real, salida estructurada forzada por gramática, y persistencia de KV cache token-exact entre sesiones.
- **Honestidad de performance**: reporta pisos reales (0.05–0.1 tok/s en hardware mínimo) en vez de ocultar el costo.

## Uso básico

```bash
# 1. Descargar pesos pre-convertidos de GLM-5.2 int4 desde Hugging Face
./setup.sh
make
COLI_MODEL=/path ./coli chat
```

Backends opcionales CUDA/Metal; UI web en TypeScript/HTML.

**Licencia**: Apache 2.0
