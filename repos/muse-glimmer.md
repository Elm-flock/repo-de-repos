---
title: muse-glimmer
url: https://huggingface.co/meta-models/Muse-Glimmer-30B
tags: [llm, multimodal, open-weights, on-device, meta, apache-2.0]
added: 2026-08-21
added_by: Emiliano
---

Modelo open-weights de ~30B de Meta Superintelligence Lab, destilado de "Muse Spark", orientado a uso agéntico y pensado para correr en una máquina propia. **No es sólo texto**: es multimodal (`image-text-to-text`), con un encoder de percepción ViT-G/14 de ~1.8B además del transformer denso.

## Por qué vale la pena

- **Corre local de verdad, con el costo medido**: K-Quant-Dynamic entra en **32 GB de VRAM con 0.2% de degradación** sobre 15 benchmarks; la variante de 17 GB entra en **24 GB con 1.0%**. A ~4-bit el LM baja de 20 GB y deja aire para KV cache + encoder + drafter.
- **Speculative decoding con drafter DFlash** (block-diffusion, bloques de 16 tokens): **RTX 5090 74.9 → 233.4 tok/s (3.1×)**, M4 Max 23.7 → 37.8 (1.5×), M5 Max 26.6 → 50.2 (1.8×). NVIDIA vía llama.cpp, Apple vía ExecuTorch.
- **Arquitectura**: ~29.6B params, 52 capas, hidden 6656, GQA 32Q/2KV (16:1), atención `[Local, Local, Local, Global]` con ventana de 2048 y RoPE θ=500k sólo en las capas locales. Contexto 131k+, vocab 202k, 100+ idiomas, hasta 4096 tokens visuales por imagen.
- **Fuerte en agéntico, flojo en computer-use**: gana en MCP Atlas **75.5** (vs 54.2 de Gemma4-31B y 62.5 de Qwen3.6-27B), DeepSearch QA 74.6, AIME 2026 94.7, SWE-Bench Pro 51.2. Pero **pierde** en OSWorld-Verified (65.9 vs 75.6) y TerminalBench 2.1 (51.7 vs 60.7).
- **Publica los números de safety aunque no lo favorezcan**: Siren AgentDojo ASR 28.4 (Gemma4 25.6 es mejor), CI Memories violation 26.4 vs 12.1 de Gemma4.
- **Ecosistema de la comunidad enorme para 12 días de vida**: el GGUF de `unsloth` tiene **más descargas que el BF16 oficial** (~865k vs ~505k). Hay MLX 4-bit para Apple, FP8/NVFP4 de RedHatAI e Inferact para NVIDIA, builds ROCm para AMD (con blog oficial de AMD para Ryzen AI Max y Radeon), y las arquitecturas ya están wired en TRL y Optimum-Intel.

## Uso básico

Variantes oficiales en la org `meta-models`: `Muse-Glimmer-30B` (BF16), `-GGUF`, `-assistant`, `-ExecuTorch-PTE`. Settings recomendados: temperature 1.0, top_p 0.95, top_k 64. El esfuerzo de razonamiento se setea en el system prompt (`Reasoning strength: low|medium|high|xhigh`). Knowledge cutoff 04-ene-2026.

**Ojo con la licencia**: el model card declara `apache-2.0`, pero el repo también incluye un `USAGE_POLICY.md`. Leerlo antes de asumir que aplican las condiciones comerciales sin restricciones de Apache-2.0 — la cobertura de prensa que dice "sin restricciones de uso" no lo tiene en cuenta.

Relacionado: [[kimi-k3]] (open-weights grande, pero infra de datacenter) y [[colibri]] para inferencia local.

**Licencia**: Apache-2.0 declarada, con `USAGE_POLICY.md` adicional en el repo
