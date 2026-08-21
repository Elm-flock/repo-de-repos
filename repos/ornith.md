---
title: ornith
url: https://github.com/ornith-ai/Ornith-1
tags: [llm, open-weights, moe, coding-agent, mit]
added: 2026-08-21
added_by: Emiliano
---

Familia de LLMs open-weight para coding agéntico cuyo truco distintivo es el **self-scaffolding**: el RL entrena al modelo para generar no sólo los rollouts de solución sino también el scaffold que los conduce, optimizando ambos en conjunto.

## Por qué vale la pena

- **4 variantes** post-entrenadas sobre Gemma 4 y Qwen 3.5: 9B-Dense, 31B-Dense, 35B-MoE y 397B-MoE. Todas con **contexto de 256K** (262.144 tokens).
- **7 checkpoints publicados** en HuggingFace, incluyendo GGUF y FP8, así que hay camino para correr local.
- **Adopción real, no sólo un anuncio**: descargas a 30 días — 9B-GGUF **4.776.368**, 35B 3.228.856, 9B 2.258.799. Es de los open-weights más bajados de su cohorte.
- **Benchmarks reportados por el vendor (397B)**: Terminal-Bench 2.1 con Terminus-2 77.5 y con harness de Claude Code 78.2; SWE-bench Verified 82.4; SWE-bench Multilingual 78.9; Claw-eval promedio 77.1.
- Integraciones documentadas: Hermes, OpenHands vía LiteLLM, llama.cpp, Ollama, Unsloth, OpenClaw, opencode.

## Uso básico

```bash
vllm serve ornith-ai/Ornith-1.0-397B --served-model-name Ornith-1.0 \
  --tensor-parallel-size 8 --max-model-len 262144 --enable-prefix-caching \
  --enable-auto-tool-choice --tool-call-parser qwen3_xml --reasoning-parser qwen3 --trust-remote-code
```

Es un modelo de razonamiento: el turno del assistant abre con un bloque `<think>`. Necesita runtimes recientes (Transformers ≥5.8.1, vLLM ≥0.19.1, SGLang ≥0.5.9) y sampling `temperature=0.6, top_p=0.95, top_k=20`. Los checkpoints de 397B piden nodo multi-GPU; sólo el 9B dense entra en una sola placa de 80 GB.

**Tres correcciones respecto del artículo con el que llegó al canal:**
1. **No es una herramienta de scaffolding ni un framework**: es una familia de modelos. El "self-scaffolding" describe cómo se entrenó, no un producto que instalás.
2. **La licencia es MIT, no Apache-2.0** como dice el blog. Verificado en el `LICENSE` de GitHub y en el campo `license` de los model cards.
3. El blog lista tres variantes y omite la 31B-Dense.

**Otras cosas a saber:**
- **El repo de GitHub no tiene código**: sólo README, LICENSE y assets. El framework de RL está descrito, no liberado. Cero releases, cero tags.
- **Dormido desde el 27-jun-2026** (~8 semanas), mientras terceros ya sirven **Ornith-1.5** — o sea la 1.0 puede estar superada sin que el repo lo refleje.
- El claim de superar a Claude Opus 4.7 queda desactualizado en su propia tabla: Opus 4.8 saca 85 en Terminal-Bench 2.1 contra 77.5, y 87.6 en SWE-bench Verified contra 82.4. También pierde contra GLM-5.2-744B en ambas variantes de Terminal-Bench.
- La org se renombró de `deepreinforce-ai` a `ornith-ai`; los links viejos redirigen.

Relacionado: [[kimi-k3]] y [[muse-glimmer]] como otros open-weights de la misma tanda.

**Licencia**: MIT
