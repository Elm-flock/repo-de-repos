---
title: pocket-tts
url: https://github.com/kyutai-labs/pocket-tts
tags: [tts, audio, cpu, kyutai, voice-cloning, mit]
added: 2026-07-20
added_by: Emiliano
---

TTS (text-to-speech) de Kyutai Labs pensado para correr en CPU sin GPU ni APIs cloud — "cabe en tu bolsillo".

## Por qué vale la pena

- **CPU-first de verdad**: ~6x tiempo real en un MacBook Air M4 usando solo 2 cores, no es un modelo grande retocado para CPU.
- **Modelo compacto**: 100M de parámetros, permite deploy local liviano.
- **Streaming**: primer chunk de audio en ~200ms, sirve para interacción responsiva (no solo batch).
- **Voice cloning**: acepta samples de audio propios; los voice states se exportan a safetensors para recargar rápido sin recomputar.
- **Multilenguaje**: inglés, francés, alemán, portugués, italiano y español.
- **Texto sin límite**: procesa inputs arbitrariamente largos.
- **Más allá de Python**: implementaciones de la comunidad en Rust, C++, C#, JS/WASM (corre en browser).

## Uso básico

```bash
pip install pocket-tts   # o: uv add pocket-tts
```

CLI con tres comandos principales: `generate` (síntesis puntual), `serve` (server web local), `export-voice` (preprocesar audio para clonar voz).

Requiere PyTorch 2.5+ y Python 3.10–3.14.

**Licencia**: MIT
