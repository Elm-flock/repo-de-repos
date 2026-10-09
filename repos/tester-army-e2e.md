---
title: tester-army-e2e
url: https://github.com/tester-army/e2e
tags: [testing, browser, mobile, typescript, apache-2.0]
added: 2026-10-09
added_by: Emiliano
---

Framework de tests end-to-end para web y mobile donde cada paso puede escribirse en lenguaje natural (`agent.act` / `agent.assert`) y mezclarse con locators y asserts clásicos en el mismo test. Lo hace TesterArmy, que además vende una plataforma comercial de testing agéntico. **Es pre-1.0 y la telemetría viene activada por defecto.**

## Por qué vale la pena

- **Replay cache**: cuando un paso del agente queda validado por un assert posterior, se graban sus acciones y la próxima corrida las repite sin llamar al modelo, hasta que la app cambie. Los tests sin pasos de agente no usan modelo.
- **Web y mobile en el mismo framework**: Playwright (Chromium, Firefox, WebKit) para web; simuladores iOS y emuladores Android vía `agent-device` de Callstack. Browsers hosteados en Kernel y simuladores hosteados en EAS.
- **Traés tu modelo** vía AI SDK: suscripciones (ChatGPT, GitHub Copilot, OpenCode Console, SuperGrok), API key o modelo local.
- **`@e2e-dev/decision`** corre `act`/`assert` con un decision model en vez de un LLM generativo; los ejemplos usan [[jev]] (`typeSafeAi.decisionModel('jev-latest')`). Jev es sólo texto y rechaza `vision: true`.
- **Ejemplos listos** para Vite, Next.js, Astro, Expo, SwiftUI, Jetpack Compose, KMP y Flutter. Reporter que comenta en PRs de GitHub y guías de CI para GitHub Actions, Bitrise, Codemagic y EAS Workflows.
- 8,3k stars a 2,5 meses de creado; último release `e2e@0.18.0` (6-oct-2026). Los docs vienen dentro del paquete (`node_modules/e2e/docs`) para que los lea un agente.

## Uso básico

```bash
npx e2e init                                    # wizard: engine web/mobile y proveedor de modelo
npm install -D @e2e-dev/decision @ai-sdk/typesafe-ai   # opcional, decision models
npx e2e telemetry disable                       # o E2E_TELEMETRY_DISABLED=1
```

Requiere Node `^22.22.3` o `>=24.8.0`.

**Trampas:**
- La API y la config pueden cambiar entre minors (lo avisa el README).
- En Windows sólo corre dentro de WSL. Los tests iOS necesitan macOS con Xcode.
- `@e2e-dev/smol` figura en el README pero no está publicado en npm.

Para testing mobile con un agente que maneja el teléfono directamente, ver [[artemis]].

**Licencia**: Apache-2.0
