---
title: wispr-flow
url: https://wisprflow.ai
tags: [speech-to-text, voice, productivity, saas]
added: 2026-10-09
added_by: Francisco
---

App de dictado con IA que transcribe en la nube y reformatea el texto según la app donde estás escribiendo. Corre en Mac, Windows, iOS y Android. **Transcribe siempre en la nube, sin modo offline, y la suscripción es cara**: Francisco la usaba y preguntó por alternativas por el precio.

## Por qué vale la pena

- **Es la referencia del rubro** contra la que se comparan las alternativas. Dice cubrir 100+ idiomas.
- **Precios** (USD por usuario/mes):
  - Free: 2.000 palabras por semana en desktop y 1.000 en mobile.
  - Pro: 15 mensual o 12 anual, dictado ilimitado. 50% off con mail educativo.
  - Growth: 23 mensual o 18 anual; 33 o 26 con Notetaker. Suma SSO/SAML, HIPAA con BAA y training bloqueado.
  - Enterprise: a medida, contrato anual. Suma SCIM, audit logs y MDM.
- **Notetaker** (sólo Mac y Windows): sus notas se pueden usar desde Claude y ChatGPT vía MCP.
- Declara SOC 2 Type II e ISO 27001.

## Uso básico

Instalador desde <https://wisprflow.ai>. No hay versión para Linux.

**Trampas:**
- **Todo el audio sale de tu máquina**: lo procesan "third-party AI providers" con zero data retention, pero no publican cuáles. El audio se borra después de transcribir, salvo que actives "Dictation cloud storage".
- **Revisá a mano "Improve the model for everyone"** en Settings > Data and Privacy. Ese setting permite entrenar con tu audio, transcripciones y ediciones. En Growth y Enterprise está apagado y bloqueado; para Free y Pro la página no dice cuál es el default.
- "Context awareness" lee el texto de la ventana activa, y las estadísticas de uso se recolectan "regardless of your data controls".

Alternativa gratis, open source y local que corre en Windows: [[handy]].

**Licencia**: SaaS propietario (Wispr AI, Inc.)
