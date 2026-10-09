---
title: handy
url: https://github.com/cjpais/Handy
tags: [speech-to-text, on-device, offline, rust, mit]
added: 2026-10-09
added_by: Denis
---

App de dictado por voz gratis, open source y 100% offline: apretás un atajo, hablás y el texto se pega en el campo que tengas en foco. Corre en Windows, macOS y Linux. Es la respuesta del canal a "¿hay algo más barato que [[wispr-flow]] para Windows?".

## Por qué vale la pena

- **Todo local**: Silero para detectar voz y transcripción en la máquina, con GPU vía Vulkan en Windows x64. El post-procesado con LLM viene apagado; si lo prendés, podés apuntarlo a Ollama local.
- **69 modelos en el catálogo** (el README está desactualizado y sólo nombra Whisper y Parakeet): Whisper de tiny a large-v3-turbo, Parakeet, Canary, Nemotron, Voxtral, Qwen3-ASR, Granite Speech, Moonshine y otros. Pesan desde ~35 MB (Moonshine Tiny) hasta ~17 GB (Voxtral Small 24B).
- **Cohere Transcribe**, el que usaba Denis en Linux: 2B params, Apache-2.0, 14 idiomas con español, ~1,8 GB en Q5_K_M. No hace streaming.
- **Todas las plataformas y arquitecturas**: Windows x64/ARM64 (.exe, .msi), macOS Intel y Apple Silicon, Linux x86_64/aarch64 (AppImage, .deb, .rpm).
- **Muy mantenido**: 33,3k stars, ~176 contributors, release cada 2-3 semanas (último v0.9.8, 3-oct-2026). Rust + Tauri v2.
- Comunidad: forks como `Melvynx/Parler`, `MaxITService/AIVORelay` (suma transcripción por API) e `info-wordcab/Handy` (detección de PII), y una extensión de Raycast.

## Uso básico

```bash
winget install cjpais.Handy           # Windows
brew install --cask handy             # macOS
sudo apt install ./Handy_*.deb        # Debian/Ubuntu (apt y no dpkg -i, para resolver dependencias)
handy --toggle-transcription          # para bindear en el WM en Wayland
```

**Trampas:**
- Wayland tiene soporte "limited": necesita `wtype`, `dotool` o `ydotool`, y en Ubuntu 26.04 `wtype` no anda. En Linux también hace falta `libgtk-layer-shell`.
- Bug conocido (#502): a veces pega el contenido anterior del portapapeles. Hay un "Reliable Paste (Beta)" en el menú de debug.
- Los paquetes de winget y Homebrew no los mantienen los devs de Handy.
- El nombre, el logo y los íconos no son open source: un fork tiene que usar otra marca.

Para transcribir reuniones en vez de dictar: [[meetily]] y [[meet2notes]]. En Linux con Hyprland, Denis ahora usa [[whispy]].

**Licencia**: MIT (código; la marca "Handy" no)
