---
title: utopiaia-translator
url: https://translator.utopiaia.com
tags: [translation, speech-to-text, tts, on-device, browser, webgpu]
added: 2026-08-10
added_by: Emiliano
---

Traductor de voz en tiempo real que corre entero en el browser sobre tu GPU: escucha, traduce y habla sin mandar nada a la nube. Versión web del "Gemma Translator", sin cuenta.

## Por qué vale la pena

- **Local y offline de verdad**: descarga ~1.5 GB de modelos la primera vez, los cachea y después funciona sin conexión. Nada de audio sale del equipo.
- **Pipeline completo en WebGPU**: Whisper-turbo para reconocimiento de voz y Kokoro para TTS — el mismo stack que usarías local, pero sin instalar nada.
- **Modo conversación con separación de voces**, así que sirve para diálogo entre dos personas y no solo para dictado.
- **Sin cuenta ni API keys**: se abre la URL y anda.
- Enfocado en habla conversacional (no documentos ni subtítulos).

## Uso básico

Abrir <https://translator.utopiaia.com> en un browser con WebGPU y esperar la descarga inicial de modelos.

No publica repo ni licencia. Relacionado: [[pocket-tts]] para el lado de síntesis de voz liviana.

**Licencia**: no declarada
