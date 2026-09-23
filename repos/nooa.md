---
title: nooa
url: https://github.com/NVIDIA-NeMo/labs-OO-Agents
tags: [agents, framework, python, nvidia, apache-2.0]
added: 2026-09-23
added_by: Guille
---

NOOA ("NVIDIA-labs Object Oriented Agents"): framework de agentes en Python donde **un agente es una clase**. Los campos son el estado, los docstrings son el prompt y los type hints son el contrato. Los métodos con cuerpo `...` los implementa un LLM en runtime, al estilo CodeAct con un REPL de Python. **Es research software en alpha (v0.0.10) y ejecuta código generado por el LLM.**

## Por qué vale la pena

- **Modelo mental de objetos para sistemas multi-agente**: cada agente tiene estado propio, métodos tipados y composición normal de Python. Guille destacó la versatilidad en proyectos de varios agentes. Emiliano: "como es Python me está mintiendo con los objetos, pero conceptualmente está mortal".
- **Benchmarks del vendor** (blog de NVIDIA, 27-jul-2026):
  - SWE-bench Verified: 82,2% con GPT-5.5 (~29 llamadas y ~1,1M tokens por tarea) y 79,8% con Opus 4.6.
  - ARC-AGI-3: 85,1% con GPT-5.6-sol.
  - CyberGym L1: 86,8%.
- **Agnóstico de modelo** vía LiteLLM: Anthropic, OpenAI, Ollama y vLLM.
- **Subpaquetes útiles**: `nooa-cli` con visor de trazas en :5001, `nooa-acp` para Zed y otros hosts de Agent Client Protocol, `nooa-memory` sobre SQLite y `nooa-bench` con Harbor.
- Tracción: 2.2k stars y 303 forks en 2 meses. Tiene paper en arXiv (2607.20709).

## Uso básico

```bash
uv add nooa   # Python >=3.12,<3.14
```

```python
class Triage(Agent, llm=get_llm_client("claude-haiku-4-5")):
    async def classify(self, ticket: str) -> str:
        """Devuelve el equipo que debe atender el ticket."""
        ...
```

**Trampas:**
- **Ejecuta código generado por el LLM, y los chequeos AST "no son un límite de contención"** (lo dice el propio repo). Correrlo en contenedor, VM o NVIDIA OpenShell.
- Alpha 0.0.x, con 127 issues abiertos: la API va a cambiar.
- Depende de LiteLLM. Fijan >=1.97.0 para evitar las versiones con backdoor (1.82.7 y 1.82.8).
- GitHub muestra la licencia como "Other" porque NVIDIA editó el apéndice del texto Apache. El `pyproject` y PyPI dicen Apache-2.0.

Relacionado: [[agent-framework]] es el framework multi-agente de Microsoft, con un enfoque de workflows en vez de objetos. [[openharness]] y [[eve]] son otros harnesses de agentes. Para aislar la ejecución: [[nono]] o [[docker-sandboxes]].

**Licencia**: Apache-2.0 (con el apéndice modificado por NVIDIA)
