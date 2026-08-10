---
title: zluda
url: https://github.com/vosen/ZLUDA
tags: [gpu, cuda, inference, rust, apache-2.0]
added: 2026-08-10
added_by: Emiliano
---

Drop-in replacement de CUDA para GPUs que no son NVIDIA: corre aplicaciones CUDA sin modificar sobre hardware AMD (y originalmente Intel, vía Level Zero) con performance cercana a nativa. Escrito en Rust por Andrzej Janik.

## Por qué vale la pena

- **No requiere tocar la app**: es una capa de traducción, no un port — el binario CUDA existente corre tal cual.
- **Relevante para inferencia local**: es la vía para usar una AMD en stacks que asumen CUDA sin esperar que cada proyecto agregue soporte ROCm.
- **Historia del proyecto que conviene conocer antes de apostar**: arrancó para Intel, después AMD lo financió, AMD cortó el financiamiento y pidió bajar el código cuando NVIDIA prohibió las capas de traducción sobre software CUDA en su EULA. El proyecto siguió como esfuerzo independiente ("back to the roots" en el update Q1&Q2 2026).
- **Sigue activo**: update Q1&Q2 2026 publicado el 29-jun-2026, con un PR de larga data agregando PhysX de 32 bits (mejor frame rate en juegos viejos que dependían de PhysX sobre AMD).

## Uso básico

Docs y builds en <https://vosen.github.io/ZLUDA/>. El sitio que circuló en Slack fue `zluda.org` (contenido de terceros); el proyecto canónico es el repo de `vosen`.

Expectativas realistas: la cobertura de la API de CUDA es parcial y varía por workload — conviene verificar el caso de uso puntual antes de planificar infra alrededor.

**Licencia**: Apache 2.0
