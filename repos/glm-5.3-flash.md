---
title: glm-5.3-flash
url: https://huggingface.co/zai-org/GLM-5.3-Flash
tags: [llm, moe, multimodal, coding-agent, open-weights, mit]
added: 2026-09-23
added_by: Denis
---

LLM MoE multimodal de Z.ai con pesos abiertos bajo MIT: entra texto, imagen y video, y sale texto. Está orientado a coding y agentes. Antes del lanzamiento se probó en forma anónima como "ox-alpha" en OpenCode y OpenRouter. **Aunque active sólo 18B, no corre en casa**: en FP8 pesa ~306 GiB.

## Por qué vale la pena

- **320B totales / 18B activos**: 288 expertos ruteados + 1 compartido, 8 activos por token. Usa atención híbrida (lineal KDA + sparse MLA con indexer) y tiene un encoder de visión de 24 capas.
- **Contexto de 1M tokens** (1.048.576). La API de Z.ai devuelve hasta 128K de salida.
- **Benchmarks del repo en HF**: 84.3 en Terminal-Bench 2.1 (medido dentro de Claude Code), 63.4 en DeepSWE y 55.3 en HLE con tools. Que "se acerca a Claude Opus 4.8" lo dice el vendor.
- **Muy barato por API**: $0.15 input / $0.50 output por millón de tokens en Z.ai. En OpenRouter (`z-ai/glm-5.3-flash`) DeepInfra lo sirve en fp4 a $0.075 / $0.25.
- **MIT de verdad**, sin gate en HF. Ojo, el hermano grande `zai-org/GLM-5.3` (~753B) usa otra licencia, que exige una revisión de seguridad a operadores de Model-as-a-Service con más de US$10B de facturación.
- En el canal lo recomendaron por experiencia directa: "una maravilla", usado desde que era ox-alpha.
- Ecosistema: GGUF de Unsloth (780K descargas) y de antirez, NVFP4 de NVIDIA y RedHatAI, y MLX.

## Uso básico

```bash
vllm serve zai-org/GLM-5.3-Flash --tensor-parallel-size 4 \
  --tool-call-parser glm47 --reasoning-parser glm47 --enable-auto-tool-choice
```

La receta oficial de vLLM es para FP8 con TP4 (4×H200 o una bandeja GB200) y por ahora pide la imagen Docker y FlashInfer ≥0.6.17. También lo soportan SGLang, TokenSpeed, Transformers, KTransformers y Unsloth. Para usarlo con agentes, lo más práctico es la API.

**Trampas:**
- **llama.cpp mainline todavía no lo soporta**: el soporte está en el PR #27754, abierto. Aun así, los GGUF van de 93 GB (IQ1_S) a 200 GB (Q4_K_XL).
- **Ollama sólo lo ofrece como `glm-5.3-flash:cloud`**, que corre en la nube de Ollama. No hay versión local.
- Durante el período stealth, OpenRouter avisó que el provider retenía prompts y completions.

Relacionado: [[colibri]] corre el GLM-5.2 grande en hardware de consumidor, streameando expertos desde disco (no soporta 5.3). Otros open-weights de coding: [[kimi-k3]], [[longcat-2]], [[ornith]]. Se probó en [[opencode]].

**Licencia**: MIT (el GLM-5.3 grande tiene licencia propia distinta)
