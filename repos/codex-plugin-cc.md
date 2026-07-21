---
title: codex-plugin-cc
url: https://github.com/openai/codex-plugin-cc
tags: [coding-agent, plugin, claude-code, codex, openai, apache-2.0]
added: 2026-07-21
added_by: Guille
---

Plugin oficial para invocar Codex desde Claude Code, tanto para revisión de código como para delegar y administrar tareas en background.

## Por qué vale la pena

- **Dos modos de revisión**: `/codex:review` hace una revisión read-only y `/codex:adversarial-review` permite orientar el análisis hacia decisiones o riesgos específicos.
- **Delegación durable**: `/codex:rescue` inicia o retoma trabajos, con opciones de ejecución foreground, espera o background.
- **Control de jobs**: suma comandos para consultar estado, recuperar resultados y cancelar tareas sin salir de Claude Code.
- **Transferencia de sesión**: convierte una conversación de Claude Code en un thread persistente que se puede continuar con `codex resume` o desde la app.
- **Mismo runtime local**: usa la instalación, autenticación, checkout y `config.toml` existentes de Codex; no crea un entorno paralelo.
- **Review gate opcional**: un hook `Stop` puede bloquear la finalización de Claude cuando Codex detecta problemas, aunque aumenta consumo y duración.

## Uso básico

```text
/plugin marketplace add openai/codex-plugin-cc
/plugin install codex@openai-codex
/reload-plugins
/codex:setup
```

Requiere Node.js 18.18 o superior y una suscripción de ChatGPT o una API key de OpenAI.

**Licencia**: Apache 2.0
