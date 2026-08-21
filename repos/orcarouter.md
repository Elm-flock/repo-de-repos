---
title: orcarouter
url: https://www.orcarouter.ai
tags: [gateway, llm, observability, saas, mit]
added: 2026-08-21
added_by: Juan Martin
---

Gateway LLM OpenAI-compatible que puntúa la dificultad de cada prompt y lo rutea al modelo más barato que pase un umbral de calidad, con guardrails, agent firewall y observabilidad encima.

## Por qué vale la pena

- **Tiene resultados publicados en un leaderboard, no sólo marketing**: **2º puesto en RouterArena** (submission 20-may-2026) con score **72.08** y **75.54% de accuracy de routing** a **USD 1.00 por 1.000 queries**. El paper es arXiv 2605.30736.
- **El algoritmo está descrito**: bandit contextual **LinUCB** sobre features léxicas + embeddings de oración, con inicialización offline por reward matrix y updates online opcionales. No es un "clasificador secreto".
- **Sin markup sobre tráfico BYOK**: pagás las tarifas publicadas del provider. El prompt caching también se factura a tarifa del provider.
- **200+ modelos** detrás de un endpoint (Claude, Gemini, GPT-5.5 Pro, DeepSeek, Grok, open-weights) con **failover mid-stream en menos de 50ms**.
- Claiman ~40% de reducción de costo de inferencia con <1% de degradación de calidad, y traen **32 packs de compliance** con evidencia exportable (GDPR, SOC 2, HIPAA, ISO 27001).
- **Hay una versión self-hosted y MIT**: `Continuum-AI-Corp/OrcaRouter-Lite` (~572 stars, Python + frontend TS) con BYOK, `model="auto"`, streaming, prompt caching cross-provider y dashboard. También hay un MCP server oficial (`orcarouter-mcp-server`).

## Uso básico

Planes: Hacker **free forever**, Team **$49/mo**, Enterprise a medida. Lanzado el 08-05-2026 por Continuum AI Corp.

**Distinción importante**: el gateway de producción es SaaS propietario y cloud-only — el paper **no** libera el código del router de producción. Lo que es open source es OrcaRouter-Lite, un router single-workspace más simple. Si lo que querés es self-hosting real, ese es el punto de entrada.

Relacionado: [[kravn]] (gateway MCP self-hosted con SSO) y [[open-connector]] (auth gateway para SaaS) cubren piezas vecinas del mismo problema.

**Licencia**: SaaS de terceros; OrcaRouter-Lite MIT
