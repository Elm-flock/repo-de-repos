---
title: jev
url: https://typesafe.ai
tags: [llm, nlp, api, saas]
added: 2026-09-23
added_by: Emiliano
---

Modelo "System One" de TypeSafe AI: no genera texto, **decide**. Le pasás un estado (texto o JSON) y preguntas tipadas, y devuelve respuestas tipadas con probabilidades. La idea es que tu código maneje el workflow y el modelo sólo conteste preguntas acotadas sobre el estado. **Es SaaS cerrado, con 8 días de vida y mejor en inglés que en español.**

## Por qué vale la pena

- **Tres tipos de pregunta, con distribución completa**:
  - `noul`: sí/no, devuelve una probabilidad de 0 a 1.
  - `choice`: hasta 255 opciones cerradas, devuelve la elegida más las probabilidades de todas.
  - `score`: escala ordenada de 2 a 10 niveles, útil para urgencia o severidad.
- **Casi gratis**: $0,042 por millón de tokens de input y el output no se cobra. En un benchmark de terceros, 500 llamadas costaron $0,008.
- **Rápido**: 236-278 ms p50 medido por terceros, y el vendor dice 70-500 ms. Sirve para ponerlo en el camino de cada request en triage, ruteo o reglas de negocio.
- **Se usa hoy por OpenRouter sin waitlist ni cuenta aparte** (`typesafe/jev-1.13`). Hay SDKs oficiales `typesafe-sdk` (PyPI) y `@typesafe-ai/sdk` (npm), ambos MIT, y una skill oficial `typesafe-ai/skills`.
- **Ecosistema en días**: `browser-use/jev-ultrafast`, una composición experimental con [[json-render]] y una alternativa open-weights, [[laya]].
- En el canal lo marcaron como candidato para triage de tickets y reglas de negocio en seguros. Dani probó integrarlo a la plataforma de agentes vía OpenRouter.

## Uso básico

```ts
const decision = await openrouter.alpha.decisions.create({
  decisionsRequest: {
    model: "~typesafe/jev-latest",
    state: "Help! My payouts have been failing for 3 days.",
    questions: {
      is_urgent: { type: "noul", instructions: "Does this message convey urgency?",
                   criteria: { true: "Explicitly time-sensitive", false: "No urgency expressed" } },
      department: { type: "choice", instructions: "Which team should handle this?",
                    criteria: { billing: "Payments, refunds", technical: "Bugs, outages", sales: "Pricing" } },
    },
  },
});
// decision.answers.is_urgent.noul -> 0..1
```

También tiene API propia (`POST https://api.typesafe.ai/v1/systemone`), en early access. No verificamos si hoy sigue con waitlist.

**Trampas:**
- **Español con precisión variable**: la doc dice que el inglés es el idioma principal de entrenamiento y que otros idiomas "se manejan, pero no igual de bien". El 90% de los workflows del equipo son en español: hay que hacer un replay contra decisiones históricas antes de confiar en él. En el canal se propuso traducir antes de preguntar.
- **Los benchmarks de "193x más rápido, 444x más barato" son del vendor**, que admite sesgos en la comparación.
- **Documenta sus propias fallas** en una página de "jaggedness": matemática, conteo, fechas, indirección y estados largos.
- Contexto de 32k para el estado más la pregunta más larga. Rate limits "ajustándose dinámicamente".
- **Los términos prohíben usar el output para entrenar o destilar un modelo competidor.** ZDR sólo para enterprise.

**Licencia**: SaaS propietario (TypeSafe AI Master Customer Agreement); los SDKs son MIT
