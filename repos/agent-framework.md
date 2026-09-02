---
title: agent-framework
url: https://github.com/microsoft/agent-framework
tags: [agents, multi-agent, framework, dotnet, microsoft, mit]
added: 2026-09-02
added_by: Emiliano
---

Framework de Microsoft para construir, orquestar y desplegar agentes y workflows multi-agente. Es el sucesor oficial declarado de Semantic Kernel **y** de AutoGen, hecho por los mismos equipos.

## Por qué vale la pena

- **No es .NET only**, aunque así llegó al canal: el mismo monorepo tiene `python/` y `dotnet/` con trenes de release separados (Python 18.6 MB vs C# 14.9 MB de código), y hay un tercer SDK en Go en `microsoft/agent-framework-go`.
- **Consolida dos linajes**: la doc de Microsoft lo dice textual — combina las abstracciones simples de AutoGen para patrones single y multi-agente con las features enterprise de Semantic Kernel (estado por sesión, type safety, filtros, telemetría).
- **Workflows basados en grafo** con checkpointing, streaming, human-in-the-loop y time-travel, en cuatro patrones: sequential, concurrent, handoff y group collaboration.
- **34 sub-paquetes en el lado Python**: `anthropic`, `claude`, `openai`, `gemini`, `bedrock`, `mistral`, `ollama`, `foundry`, `foundry_local`, `devui`, `a2a`, `ag-ui`, `redis`, `mem0`, `purview`, entre otros.
- **GA desde el 2-abr-2026** para Python y .NET, con 13.294 stars, 222 contributors y más de 100 releases. Última .NET `dotnet-1.20.0` (31-ago-2026), última Python `python-1.16.0` (28-ago-2026).
- OpenTelemetry integrado, agentes declarativos en YAML, DevUI, y AF Labs para benchmarking y RL.

## Uso básico

```bash
pip install agent-framework                      # Python: instala todos los sub-paquetes
dotnet add package Microsoft.Agents.AI           # .NET
dotnet add package Microsoft.Agents.AI.Foundry
go get github.com/microsoft/agent-framework-go   # Go (preview)
```

## Advertencias

- **Churn altísimo pese al 1.x GA**: 505 issues abiertos sobre 2.799 cerrados, 145 PRs abiertos sobre 4.155. La API se mueve rápido.
- **Dos trenes de versión desacoplados** (.NET 1.20 vs Python 1.16): una feature puede existir en un lenguaje y no en el otro, y los samples se desfasan entre ellos.
- **Gravedad Azure fuerte**: se puede usar con cualquier provider, pero los quickstarts del README y de Learn asumen Foundry con `AzureCliCredential`/`DefaultAzureCredential`. Microsoft además aclara explícitamente que usarlo con "Third-Party Systems" (modelos o agentes no-Azure) es a tu propio riesgo.
- **El SDK de Go es public preview** con features ausentes (declarative agents, RAG, CodeAct, functional workflows) y sus issues van a otro repo.
- **Qué pasa con los predecesores**: ninguno está archivado, pero `microsoft/autogen` (60.7k stars) no tiene push desde el 15-abr-2026 — está de hecho en wind-down. `microsoft/semantic-kernel` (28.5k stars) sigue activo. Si arrancás algo nuevo, este es el camino; si tenés algo en AutoGen, hay guía de migración oficial.
- Algunos paquetes siguen en alpha (ej. `python-hosting-a2a-1.0.0a260723`).

Relacionado: [[anthropic-sdk-csharp]] si el stack es .NET, [[openharness]] y [[agenticros]] del lado de harnesses de agentes, [[power-platform-skills]] para el resto del ecosistema Microsoft.

**Licencia**: MIT
