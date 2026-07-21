---
title: odysseus
url: https://github.com/odysseus-dev/odysseus
tags: [llm, agents, self-hosted, docker, odysseus-dev, agpl-3.0]
added: 2026-07-21
added_by: Lucas
---

Workspace de IA self-hosted que reúne chat, agentes, investigación, documentos, correo, notas, calendario y modelos locales en una sola interfaz.

## Por qué vale la pena

- **Workspace integrado**: combina agentes con tools, MCP, archivos, shell, skills y memoria con edición de documentos y gestión personal.
- **Modelos locales o por API**: incluye recomendaciones según hardware, descarga y serving de modelos para armar flujos locales.
- **Deep Research incluido**: ejecuta investigación web multi-step, lee fuentes y produce reportes dentro del mismo entorno.
- **Herramientas de productividad reales**: integra correo IMAP/SMTP, notas, tareas, recordatorios, calendario y sincronización CalDAV.
- **Comparación de modelos**: permite pruebas ciegas lado a lado y una síntesis posterior de los resultados.
- **Despliegue autocontenido**: Docker Compose levanta el servicio y expone la interfaz en el puerto 7000; también documenta instalación nativa y GPU.
- **Historial rastreable**: el enlace compartido originalmente, `pewdiepie-archdaemon/odysseus`, redirige a la organización canónica actual `odysseus-dev`.

## Uso básico

```bash
git clone https://github.com/odysseus-dev/odysseus.git
cd odysseus
cp .env.example .env
docker compose up -d --build
```

La contraseña inicial de administrador aparece en `docker compose logs odysseus`.

**Licencia**: AGPL 3.0 o posterior
