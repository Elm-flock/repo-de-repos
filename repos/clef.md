---
title: clef
url: https://huggingface.co/Cloudflare/clef
tags: [nlp, inference, open-weights, cloudflare, apache-2.0]
added: 2026-10-09
added_by: Juan Martin
---

Familia de "decision models" de Cloudflare compatible con la API de [[jev]]: recibe un `state` (texto, JSON, imágenes o video) y preguntas tipadas (`noul`, `choice`, `score`), y devuelve probabilidades por opción en un solo forward pass, sin generar texto. Se usa hoy en Workers AI y tiene pesos abiertos. **Todos los benchmarks los corrió Cloudflare, y con GGUF se pierde la visión.**

## Por qué vale la pena

- **Lo que Jev no tiene**: encoder de visión (Jev es sólo texto) y 64k de contexto, contra 32k.
- **Dos tamaños, pesos Apache-2.0 sin gate**: `clef` (27,4B, base Qwen3.8-27B) y `clef-flash` (9,4B, base Qwen3.5-9B). Backbone congelado que sólo hace prefill, más un "joint schema head" con adapters LoRA rank-256.
- **Latencia auto-reportada**: mediana de 209 ms (Clef) y 39 ms (Clef-flash), contra 524 ms de Jev.
- **Calidad mixta contra Jev, también auto-reportada**: gana en BANKING77 (94,2 vs 79,7), CLINC150 (97,4 vs 89,3) y BFCL (98,5 vs 95,8); pierde en When2Call (72,4 vs 81,0), GPQA Diamond (48,0 vs 78,3), ANLI y NLI4CT.
- **Precio en Workers AI**: USD 0,24 (Clef) y USD 0,09 (Clef-flash) por millón de tokens de entrada.
- **Comunidad en una semana**: GGUF de `ggml-org` y `bartowski`, MLX 4/8 bit, NVFP4, FP8, EXL3 y finetunes como `TextCortex/clef-cybersecurity`. llama.cpp lo soporta desde el PR #29831 (3-oct-2026), sólo texto.

## Uso básico

```js
// En un Worker
await env.AI.run("@cf/cloudflare/clef", {
  model: "clef",
  state: "Help! My payouts have been failing for 3 days.",
  questions: {
    urgent: { type: "noul", instructions: "Is this urgent?" },
    team: { type: "choice", instructions: "Which team?", criteria: { billing: "...", technical: "..." } },
  },
});
```

```bash
llama serve -hf ggml-org/Clef-GGUF    # local, sólo texto
```

En Python, el repo de HF trae `joint_schema_model.py`; `systemone(model, processor, body)` acepta el mismo body que `POST /v1/systemone` de Jev.

**Trampas:**
- El script de HF usa `max_length=16384` por defecto: los 64k son la cifra de Workers AI, en local hay que subirlo a mano.
- El modelo de 27B en BF16 pide una GPU grande. Para correr chico y local, ver [[laya]].
- No encontramos un `decisionModel` para Clef en el provider de AI SDK de Workers AI, así que no está verificado que se enchufe en [[tester-army-e2e]] como Jev.
- El fine-tuning por RL es sólo con el equipo FDE de Cloudflare, por formulario.

**Licencia**: Apache-2.0 (pesos); el uso en Workers AI se rige por los términos de Cloudflare
