---
title: ai-avatar-system
url: https://github.com/PunithVT/ai-avatar-system
tags: [generative, voice-cloning, self-hosted, python, mit]
added: 2026-09-02
added_by: Emiliano
---

Plataforma self-hosted de avatar / humano digital: subís una foto, clonás una voz y conversás en tiempo real con lip-sync generado por respuesta. **Ojo que es un proyecto de un solo autor con el README sobrevendido** — ver advertencias antes de invertir tiempo.

## Por qué vale la pena

- **El pipeline completo es open source y MIT limpia**: faster-whisper → Claude/GPT-4o/Ollama → Chatterbox Multilingual TTS → MuseTalk V1.5, con los chunks de video llegando por WebSocket.
- **Puede correr sin cloud**: el paso de LLM acepta Ollama, así que se puede armar todo on-premise.
- **Infra realista para levantarlo**: FastAPI + Next.js 14 + PostgreSQL 15 + Redis 7 + Celery + nginx, con Docker Compose y hasta Terraform (`HCL`) en el repo.
- Arranca con un `docker compose up -d`; los ~9 GB de modelos de MuseTalk son un paso aparte y opcional.

## Uso básico

```bash
git clone https://github.com/PunithVT/ai-avatar-system.git && cd ai-avatar-system
cp .env.example .env && docker compose up -d    # frontend :3000, API :8000
bash scripts/setup_musetalk.sh                  # ~9 GB de modelos, opcional
# luego AVATAR_ENGINE=musetalk en .env y docker compose restart backend
```

## Advertencias — son varias y pesan

- **El README miente sobre las imágenes prebuilt**: dice que se publican en `ghcr.io/punithvt/ai-avatar-system-backend` "en cada release", pero el workflow dispara solo con tags `v*` y **el repo no tiene ni un tag ni un release**. Esas imágenes no existen; hay que buildear.
- **CI roto**: la última corrida en `main` fue el 23-mar-2026 y falló. Las dos de julio en ramas de feature también.
- **Parado y con bus factor 1**: último commit el 29-jul-2026, 3 contributors de los cuales uno hizo 135 de los 139 commits.
- **Los 30 FPS no son un benchmark propio**: el README los atribuye al paper de MuseTalk (arXiv 2410.10122). Lo que sí declara para sí mismo es bastante peor: 30-90 s por oración en CPU y ~60 s (GPU) o ~5 min (CPU) de warm-up del worker.
- **Hardware caro para uso real**: recomienda un `g5.xlarge` (A10G, 24 GB), ~$0.30/hr spot ≈ $72/mes a 8 h/día, más 9 GB de modelos.
- **Incoherencia interna**: el diagrama de arquitectura sigue listando XTTS v2 mientras la tabla de features y el changelog dicen que Chatterbox lo reemplazó en mar-2026.
- **Tracción sospechosa**: 467 stars contra 6 watchers reales, 3 contributors y 107 forks todos inertes (mismo `pushed_at` que el upstream) es una proporción anómala.
- Sin demo ni instancia hosted. Y el README se autodenomina "el único proyecto del nicho que podés shippear como producto", cosa que no se puede verificar.

Relacionado: [[pocket-tts]] para TTS liviano, [[minimax-h3]] para generación de video, [[openshorts]] para el lado de edición.

**Licencia**: MIT
