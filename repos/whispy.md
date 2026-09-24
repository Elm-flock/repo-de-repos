---
title: whispy
url: https://github.com/Ceereals/whispy
tags: [speech-to-text, on-device, rust, hyprland, mit]
added: 2026-09-24
added_by: Denis
---

Dictado push-to-talk local para Hyprland: apretás una tecla, hablás, y el texto se escribe en el campo con foco. Un daemon en Rust mantiene un modelo de whisper.cpp cargado en RAM, un cliente liviano se dispara desde los binds y una "pill" de Quickshell muestra el estado. El audio nunca sale de la máquina.

## Por qué vale la pena

- **Sin cold start**: `whispy-daemon` supervisa un `whisper-server` hijo con el modelo residente y le habla por HTTP en localhost; el cliente es un binario Rust elegido para arrancar en <10 ms (el autor lo descartó en Python por la latencia de hotkey).
- **Vulkan en AMD sin ROCm**: desarrollado en RX 9070 XT (RDNA4). Con `large-v3-turbo-q5_0` (modelo por defecto) transcribe clips de 13-34 s en 0,52-0,86 s, más rápido que `medium-q5_0` (0,69-1,31 s) y mejor en code-switching con términos técnicos (Next.js, Vercel, Elasticsearch). Sin GPU cae a CPU, con OpenBLAS ~3-4× más rápido.
- **Filtro de alucinaciones**: descarta segmentos con `no_speech_prob > 0.6` o `avg_logprob < -1.0` y los que matchean una blacklist con fuzzy match (umbral 0.85). `whispy-daemon stats` resume clips aceptados vs descartados por motivo para ajustar umbrales.
- **Dos modos de inyección**: `paste` (default: `wl-copy` + Ctrl+V vía `ydotool`, guarda y restaura el portapapeles, conserva tildes) y `type` (`wtype`, funciona en terminales y no toca el portapapeles).
- **Post-procesado con LLM opcional**: workflows que reescriben la transcripción antes de inyectarla contra cualquier endpoint OpenAI-compatible (default: ollama local). Se eligen con `--workflow NAME` o solos según la clase de la ventana con foco.
- **Vocabulario, correcciones y snippets**: sesgar a whisper hacia nombres propios, autocorregir errores recurrentes (`"hyperland" = "Hyprland"`) y expansiones de texto con `{{DATE}}`, `{{TIME}}`, `{{CLIPBOARD}}`.
- **No solo Hyprland**: el dictado también anda en X11 y Wayland genérico (GNOME, KDE, Sway, XFCE, i3) con `xdotool`/`xclip`; ahí la pill se reemplaza por notificaciones de escritorio.
- **Alternativas que el autor evaluó y descartó** (`docs/spike-fork-vs-build.md`): nerd-dictation (sin daemon, atado a VOSK), Handy, OpenWhispr y Whispering (apps GUI monolíticas sin estado consumible desde afuera), hyprwhspr y whisper_dictation (daemon + cliente, pero con faster-whisper/python-whisper).

## Advertencia

Proyecto de un solo autor armado en 3 días: v0.1.0 y v0.2.0 salieron el 28 y 29 de mayo de 2026 y no tuvo commits después. El benchmark de WER es cualitativo, sobre muestras en italiano/inglés. Sin backend CUDA: en NVIDIA hay que compilar whisper.cpp a mano y apuntar `stt.server_bin` al binario.

## Uso básico

```sh
paru -S whispy            # Arch/CachyOS; en otras distros: ./install.sh
whispy-daemon setup       # compila whisper.cpp, baja el modelo, configura ydotool y servicios systemd
```

Binds en Hyprland (toggle para empezar y terminar, Escape cancela):

```ini
bind = SUPER ALT, Space, exec, whispy-client toggle
bind = , Escape, exec, whispy-client cancel
```

`whispy-daemon setup doctor` lista las dependencias que necesita tu sesión; `whispy-daemon setup verify` chequea que modelo, daemon, `ydotoold` y `whisper-server` estén arriba.

**Licencia**: MIT
