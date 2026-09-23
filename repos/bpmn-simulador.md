---
title: bpmn-simulador
url: https://github.com/christianivan42-dotcom/BPMN-Simulador
tags: [simulation, automation, llm, python, typescript, mit]
added: 2026-09-23
added_by: Emiliano
---

App web en español para modelar procesos en BPMN 2.0 (AS-IS y TO-BE), simularlos con un motor de eventos discretos y pedirle a un LLM que interprete los resultados y proponga mejoras. **Es un prototipo personal: 8 stars, 1 solo commit, sin releases ni CI.**

## Por qué vale la pena

- **Cubre un nicho poco explorado con LLMs**: el LLM no sólo dibuja el diagrama, también interpreta la simulación. Sirve para comparar un proceso actual contra uno rediseñado con números, no a ojo.
- **Motor de simulación en el browser** (`simEngine.ts`): 7 distribuciones de probabilidad, turnos 24/7, costos, animación de tokens y export a Excel. El backend suma Monte Carlo y teoría de colas.
- **LLMs con fallback en cadena**: Gemini (`gemini-2.5-flash` por defecto), Groq (`llama-4-scout-17b`), DeepSeek y Ollama local. **Funciona sin API key**, en un "modo demo / análisis calculado".
- Stack conocido: FastAPI + SQLAlchemy + Alembic con SQLite por defecto, y React 18 + Vite 8 + bpmn-js 17. Postgres, Qdrant y OpenTelemetry son opcionales.
- En el thread del canal apareció otro uso: modelar como BPMN los procesos de agentes para definirles mejor las tareas y verlos gráficamente.

## Uso básico

```bash
git clone https://github.com/christianivan42-dotcom/BPMN-Simulador && cd BPMN-Simulador
bash scripts/start-dev.sh    # backend :8010 + frontend :5173
```

Requiere Python 3.11+ y Node 20.19+ o 22.12+. Opcional: `GEMINI_API_KEY` en `backend/.env`.

**Trampas:**
- **Madurez de demo**: la historia se reescribió en un único commit de +42.500 líneas (11-sep-2026). El autor tiene una cuenta de 4 meses, y hay restos de otro proyecto (`agente-ia-prueba-frontend` en el `package.json`, un seed de un caso puntual, `<tu-usuario>` en el README). No hay versiones para fijar.
- Los resultados de simulación se guardan en el `localStorage` del browser.
- El README declara 27 tests de backend y 99 de frontend. No los corrimos.
- **bpmn-js no es MIT puro**: su licencia exige dejar visible y sin modificar la marca de agua de bpmn.io en los diagramas renderizados. Importa si se quiere meter en un producto.

Relacionado: [[agent-framework]] modela workflows multi-agente como grafos en código (el uso "BPM para agentes" del thread), [[logfire]] si se activa el tracing con OpenTelemetry.

**Licencia**: MIT (copyright "2026 CIEC"; la dependencia bpmn-js tiene licencia bpmn.io con marca de agua obligatoria)
