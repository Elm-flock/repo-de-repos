---
title: planttalk
url: https://github.com/openai/planttalk
tags: [realtime, voice, iot, typescript, openai, apache-2.0]
added: 2026-07-21
added_by: Guille
---

Proyecto de referencia de OpenAI para conversar por voz con una planta usando ChatGPT, cámara y micrófono, con sensores Arduino opcionales.

## Por qué vale la pena

- **Demo multimodal completa**: combina observaciones de cámara, conversación por voz en tiempo real e historial reciente en un dashboard web.
- **Hardware mínimo accesible**: funciona con una computadora, webcam y micrófono; el microcontrolador no es obligatorio.
- **Sensores con utilidad concreta**: la versión completa suma humedad de suelo y luz por USB serial para evitar depender sólo de la imagen.
- **Pensado para modificar**: documenta puntos de extensión para voz, personalidad, recordatorios, nuevos sensores, salud a largo plazo y uso educativo.
- **Construcción guiada por Codex**: el README propone que Codex lea el repo y acompañe el cableado, setup y adaptación al hardware disponible.
- **Stack web inspeccionable**: el dashboard permite seleccionar cámara, observar, conectar Arduino, iniciar la conversación y pasar a modo ambiente.

## Uso básico

Abrir Codex Desktop y pedir:

```text
Help me make Plant Talk https://github.com/openai/planttalk
```

Requiere Chrome o Edge, acceso a la API de OpenAI, webcam, micrófono y parlantes. Arduino y los sensores son opcionales.

**Licencia**: Apache 2.0
