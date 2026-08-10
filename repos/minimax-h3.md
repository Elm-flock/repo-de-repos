---
title: minimax-h3
url: https://fal.ai/minimax-h3
tags: [video, generative, multimodal, minimax, open-weights]
added: 2026-08-10
added_by: Emiliano
---

Modelo multimodal de generación y edición de video de MiniMax, liberado con pesos abiertos el 31-jul-2026. Lee texto, imagen, video y audio en un mismo contexto unificado y produce contenido audiovisual completo en un solo pase end-to-end.

## Por qué vale la pena

- **Clips de 5 a 15 segundos en 2K a 24 FPS con audio estéreo nativo** en cada generación — el audio no es un segundo pase pegado después.
- **Open-weights** en una categoría (video generativo de calidad) donde casi todo lo bueno es cerrado.
- **Contexto multimodal unificado**: interpreta intención creativa cruzando modalidades en vez de tener un endpoint por tipo de input.
- **Tres endpoints en fal** desde el día 0: text-to-video, image-to-video y reference-to-video, así que se integra con una API call sin aprovisionar GPUs.
- **Precio**: USD 0.26 por segundo de output 2K, sin suscripción.

## Uso básico

API hosteada en fal (`fal.ai/models/minimax/h3/...`) — fal fue partner oficial de lanzamiento. Los pesos abiertos permiten self-host si tenés el hardware.

**Licencia**: open weights — verificar los términos en el release de MiniMax.
