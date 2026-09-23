---
title: off-grid
url: https://github.com/off-grid-ai/OGAM
tags: [on-device, offline, mobile, llm, typescript, mit]
added: 2026-09-23
added_by: Emiliano
---

App móvil (Android e iOS) para correr IA completamente offline en el teléfono: chat con cualquier GGUF, visión, voz a texto con Whisper, Stable Diffusion, tool calling y RAG local. Sin cuenta ni API key. **Es open core**: el tier Pro es pago y su código está en un repo privado.

## Por qué vale la pena

- **Todo el stack local en una sola app**: llama.cpp (vía `llama.rn`), Whisper (`whisper.rn`) y Stable Diffusion. En Android usa MNN con NPU Snapdragon y en iOS Core ML.
- **Performance declarada** (Snapdragon 8 Gen 2/3 y A17 Pro, sin verificación independiente): 15-30 tok/s en CPU en un flagship, 20-40 tok/s con GPU Adreno vía OpenCL, imágenes en 5-10 s con NPU y visión en ~7 s.
- **Modelos**: Qwen 3, Llama 3.2, Gemma 3, Phi-4 o cualquier GGUF. Visión con SmolVLM, Qwen3-VL y Gemma 3n. Más de 20 modelos de SD.
- **Está en las tiendas**: Play Store con 50K+ descargas y App Store (iOS 17+). También hay APK directo en GitHub.
- Se puede conectar a servidores compatibles OpenAI (Ollama, LM Studio, LocalAI) cuando el teléfono no alcanza.
- Tracción: 3.1k stars y más de 100 releases desde feb-2026. La misma org tiene una versión desktop (`OGAD`, AGPL-3.0) con gateway compatible OpenAI.

## Uso básico

Instalar desde Play Store / App Store, o bajar el APK de <https://github.com/off-grid-ai/OGAM/releases/latest>. Desde fuente:

```bash
git clone https://github.com/off-grid-ai/OGAM.git && cd OGAM && npm install
npm run android
```

**Trampas:**
- **El post que lo trajo al canal está desactualizado**: dice "sin suscripción", pero existe Pro ($69 de por vida o $49/año, con TTS Kokoro, personas, acciones MCP y sync con Mac). También dice que en iOS hay que compilar, pero ya está en App Store.
- No verificamos que compile sin el submódulo privado `pro`.
- Versión 0.0.x, depende de un `llama.rn` en release candidate y tiene 147 issues abiertos. La App Store le da 3,2★.
- El NPU Hexagon es experimental: sólo acelera Q4_0/Q8_0, las K-quants caen a CPU y algunas arquitecturas dan output roto.
- El repo se llamaba `alichherawalla/off-grid-mobile`; el link viejo redirige.

Relacionado: [[litert-js]] y [[utopiaia-translator]] también corren modelos on-device, pero en el browser. [[gemma-translator]] es otro caso fully offline.

**Licencia**: MIT (el tier Pro es código privado y pago)
