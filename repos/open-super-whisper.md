---
title: open-super-whisper
url: https://github.com/TakanariShimbo/open-super-whisper
tags: [speech-to-text, openai, python, mit]
added: 2026-10-09
added_by: Dani
---

GUI de escritorio en PyQt6 que graba con un atajo global y transcribe con la API de OpenAI, inspirada en Superwhisper. **Abandonado desde abril de 2025, sin opción local, y guarda la API key sin cifrar.** Se compartió como opción para Windows; para dictado gratis y local, [[handy]] es mejor en todo.

## Por qué vale la pena

- **Un `.exe` y listo** en Windows: release único v1.0.0 (abr-2025), ~67 MB armado con PyInstaller.
- **Modelos de OpenAI**: `whisper-1`, `gpt-4o-transcribe` y `gpt-4o-mini-transcribe`, hardcodeados.
- **Vocabulario custom e instrucciones de sistema**, que se mandan como prompt a la API de transcripción.

## Uso básico

Bajar `OpenSuperWhisper.exe` desde Releases, o desde el código:

```bash
uv sync && python main.py --minimized   # Python >= 3.11; atajo por defecto Ctrl+Shift+R
```

**Trampas:**
- Requiere una API key paga de OpenAI y todo el audio va a OpenAI.
- La key se guarda en texto plano con `QSettings`; en Windows termina en el registro.
- No pega solo: copia al portapapeles y hay que hacer Ctrl+V.
- 32 stars, un solo autor, sin commits en ~17 meses. Binario sólo para Windows; en macOS hay que correrlo desde el código.
- **No confundir con `Starmel/OpenSuperWhisper`**: otro proyecto, app nativa en Swift sólo para macOS, MIT, 3k stars y activo. Si lo que buscás es la versión de Mac, probablemente sea esa.

**Licencia**: MIT
