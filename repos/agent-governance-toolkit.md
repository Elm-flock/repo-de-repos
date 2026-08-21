---
title: agent-governance-toolkit
url: https://github.com/microsoft/agent-governance-toolkit
tags: [security, agents, sandbox, python, microsoft, mit]
added: 2026-08-21
added_by: Emiliano
---

Toolkit de governance para agentes autónomos: enforcement determinístico a nivel aplicación, identidad zero-trust, sandboxing de ejecución y tooling de SRE. Intercepta los tool calls antes de que la intención salga a la red, en vez de confiar en safety a nivel prompt.

## Por qué vale la pena

- **Enforcement determinístico, no probabilístico**: el core de decisión de políticas está en Rust, es stateless y fail-closed. No depende de que el modelo "se porte bien".
- **10 especificaciones formales RFC 2119** respaldadas por **992 tests de conformance** y 29 ADRs. Por spec: Audit & Compliance 157 tests, AgentMesh Identity/Trust 135, MCP Security Gateway 127, Agent SRE 111, Hypervisor Execution Control 80.
- **MCP Security Gateway**: detecta tool poisoning, schema drift, typosquatting de herramientas e inyección de instrucciones ocultas — los ataques concretos que aparecen al conectar MCP servers de terceros.
- **Sandbox de 4 anillos de privilegio** + capa SRE con kill switch, monitoreo de SLO/error budget, circuit breakers y chaos testing.
- **Cubre 10/10 del OWASP Agentic Top 10**, AARM R1–R9 y los 5 elementos ATF. Tiene OpenSSF Scorecard + Best Practices badge y ClusterFuzzLite con 7 fuzz targets.
- **5 SDKs**: PyPI `agent-governance-toolkit` 4.1.0, npm `@microsoft/agent-governance-sdk` 5.0.0, NuGet `Microsoft.AgentGovernance`, Rust y Go. Adapters para Microsoft Agent Framework, Semantic Kernel, AutoGen, LangGraph y CrewAI.
- Se instala como **plugin de Claude Code**: `/plugin install agt-governance@agent-governance-toolkit`.
- ~6k stars, último push 19-ago-2026. README traducido a inglés, japonés, chino simplificado y coreano.

## Uso básico

```bash
pip install "agent-governance-toolkit[full]"   # Python 3.11+
```

```python
from agentmesh.governance import govern

safe_tool = govern(my_tool, policy="policy.yaml")   # levanta GovernanceDenied si viola
```

**Dos trampas**: el wheel base instala **sólo el CLI de compliance** — hay que pedir el extra `[full]` para los módulos de governance. Y los imports `agent_os` emiten `DeprecationWarning` (la distribución vieja `agent-os-kernel` quedó deprecada); `agt-policies` hace la migración one-way v4→v5.

Está en **Public Preview**: puede haber cambios que rompan antes del GA.

Relacionado: [[visa-vulnerability-agentic-harness]] para el lado ofensivo/SAST, [[mcpwasm]] para sandboxing de MCP vía WASM.

**Licencia**: MIT
