---
title: artemis
url: https://github.com/google/artemis
tags: [testing, mobile, mcp, python, google, apache-2.0]
added: 2026-10-09
added_by: Emiliano
---

Agente de Google que traduce instrucciones en lenguaje natural a automatización de dispositivos Android: tests E2E, exploración y reproducción de bugs. Trae un servidor MCP para que Claude Code, Codex, Cursor o Windsurf manejen un teléfono real. **Sólo Android, sin releases, casi un único mantenedor, y depende en la práctica de modelos Gemini.**

## Por qué vale la pena

- **Dos perfiles**: Flash es un loop reactivo de un solo modelo (~3-5 s por paso); Pro es un grafo multi-agente en LangGraph (Planner, Operator, Checker y un safety net antes de cada acción), ~15-40 s por paso.
- **AndroidWorld "99%+"** de tareas completadas sobre más de 100 tareas multi-paso. Es auto-reportado (badge e imagen de leaderboard en el repo).
- **Cuatro formas de usarlo**: consola web en `localhost:8000`, CLI, servidor MCP y SDK Python (`artemis-client`).
- Modelos por defecto: `gemini-3.8-flash`, `gemini-robotics-er-2-preview` para localizar por coordenadas y `gemini-3.5-flash-lite` para el safety net. También soporta OpenAI, Anthropic, OpenRouter, xAI y `llama3.2-vision`.
- 11,2k stars y 1,1k forks en dos meses. Hay un PR comunitario abierto (#175) con soporte nativo de iOS, sin mergear.
- En el canal lo vieron como la forma de que el agente de QA interno teste mobile "por las buenas", en vez de TeamViewer más desktop use.

## Uso básico

```bash
git clone https://github.com/google/artemis.git && cd artemis && ./start.sh   # Windows: .\start.bat
uv run artemis run "Open Settings, find Battery and tell me current level" --profile flash
uv run artemis mcp --install claude    # o --install all
```

`start.sh` instala ADB, scrcpy, FFmpeg y las dependencias de uv. Necesita al menos una API key de LLM.

**Trampas:**
- **No lo instales desde PyPI**: `artemis` y `artemis-client` en PyPI son proyectos ajenos. Hay que instalar desde git.
- Instala en el teléfono una APK propia ("Artemis Accessibility Helper", un servicio de accesibilidad), salvo que pongas `ARTEMIS_HELPER_AUTO_INSTALL=false`.
- Está en la org `google` con copyright de Google, pero no hay señales de producto con soporte: sin releases ni tags, y un mantenedor con 109 commits contra 1-4 del resto.

Para tests E2E web + mobile con replay cache, ver [[tester-army-e2e]]. Para darle expertise mobile a un agente de código, [[mobiai-core]].

**Licencia**: Apache-2.0 (incluye partes de `minitap-ai/mobile-use`, también Apache-2.0)
