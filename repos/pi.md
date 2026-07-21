---
title: pi
url: https://github.com/earendil-works/pi
tags: [llm, cli, coding-agent, typescript, earendil-works, mit]
added: 2026-07-21
added_by: Emiliano
---

Agent harness para terminal que combina un agente de código extensible, una API unificada para LLMs, un runtime de agentes y una librería TUI en un monorepo TypeScript.

## Por qué vale la pena

- **Cuatro piezas reutilizables**: publica paquetes separados para el coding agent, el loop con tool calling y estado, la API multi-provider y la TUI con renderizado diferencial.
- **Extensible sin modificar el core**: admite extensions TypeScript, skills, prompt templates, temas y paquetes instalables desde npm o Git.
- **Muchos proveedores en una interfaz**: soporta suscripciones de Claude, ChatGPT/Codex y GitHub Copilot, además de APIs de OpenAI, Anthropic, Gemini, DeepSeek, NVIDIA NIM, OpenRouter, Mistral y otros.
- **Cuatro modos de integración**: interactivo, salida texto/JSON, RPC por JSONL y SDK embebible.
- **Historial rastreable**: el enlace compartido originalmente, `badlogic/pi-mono`, redirige al repo canónico actual `earendil-works/pi`.
- **Límite de seguridad explícito**: no trae permisos restrictivos por defecto; para aislar tools y comandos recomienda contenedor, micro-VM o un sandbox externo.

## Uso básico

```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
pi /login
pi
```

También se puede instalar con el script de `pi.dev` y ejecutar en modo no interactivo con `pi -p "prompt"`.

**Licencia**: MIT
