---
title: kimi-k3
url: https://huggingface.co/moonshotai/Kimi-K3
tags: [llm, moe, multimodal, moonshot, open-weights]
added: 2026-07-30
added_by: Emiliano
---

LLM open-weight multimodal (texto + imágenes + video) de arquitectura MoE, clase multi-billón de parámetros, de Moonshot AI. Orientado a coding de larga duración, agentes, research y automatización enterprise. Sucesor de Kimi-K2 (pesos publicados el 27-jul-2026).

## Por qué vale la pena

- **~2.8T parámetros totales, 104B activados por token** (MoE): probablemente el open-weight más grande liberado a la fecha.
- **MoE de 896 expertos** totales, 16 por token + 2 shared; framework "Stable LatentMoE" (~2.5× mejor eficiencia de escalado).
- **Contexto de 1M tokens** (1.048.576).
- **Multimodal nativo** con encoder de visión MoonViT-V2 (401M params).
- **Benchmarks reportados**: 93.5 GPQA Diamond, 88.3 Terminal-Bench 2.1, 91.2 BrowseComp (frontier-level).

## Uso básico

Pesos en MXFP4 con activaciones MXFP8 (quantization-aware training); engines recomendados vLLM, SGLang, TokenSpeed. **Advertencia**: a 2.8T params es infra de datacenter (multi-GPU), no corre en una workstation típica. El previo `moonshotai/Kimi-K2` está en la misma org.

**Licencia**: "Kimi K3 License" (open weights, licencia propia — no OSI estándar)
