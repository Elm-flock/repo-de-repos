---
title: laya
url: https://github.com/NandhaKishorM/laya
tags: [nlp, inference, open-weights, python, apache-2.0]
added: 2026-09-23
added_by: Tomas
---

Alternativa open-weights a [[jev]]: motor de decisiones tipadas (`choice` / `score` / `noul`) que responde con probabilidades en un solo forward pass, sin generar tokens, y corre local. Lo hace Nandakishor M (Convai Innovations). **Tiene 5 días de vida y, sin fine-tune, rinde bastante por debajo de Jev.**

## Por qué vale la pena

- **Mismo contrato que Jev**: `laya-serve` expone `POST /v1/systemone` con el mismo formato de respuesta. Según el README, un cliente de Jev funciona cambiando sólo el `baseUrl` (no lo probamos).
- **Chico y local**: el checkpoint en inglés usa ModernBERT-large (421M params, 843 MB) y el multilingual mmBERT-base (322M, 644 MB). En una T4 tarda ~33-40 ms por pregunta, 7,2 ms en batch de 10. Sin costo por llamada ni datos que salgan de la máquina.
- **Contra Jev, en un benchmark de terceros** (500 ejemplos, Laya 0.3.4 contra jev-1.13): Jev gana en precisión (76,4% vs 66,8%) y en calibración. Laya gana en latencia (45 ms vs 278 ms p50, y ~190 ms del valor de Jev es red).
- **Hay checkpoint multilingual que declara español.** En MASSIVE intent con 20 opciones (azar = 0,05), en español saca 0,53, contra 0,82 del checkpoint inglés en inglés.
- Pesos públicos sin gate, Apache-2.0 en código, PyPI y los tres modelos de HF (con tag `commercial-use`).
- Comunidad: un Space de HF con Gradio, `laya-adk-toolkit` para Google ADK y un fine-tune para browser-use. La landing <https://brainfunctioncollapse.com/laya> que se compartió en el canal es de un tercero (Wojciech Dobry, repo `wdobry/laya-playground`).

## Uso básico

```bash
pip install laya                          # o: uv pip install laya
pip install "laya[serve]" && laya-serve   # servidor compatible con Jev en :8000
```

```python
from laya import Router
Router(default="multilingual").predict(state, questions)
```

**Trampas:**
- **Sin fine-tune está casi al nivel del azar**: los checkpoints base sacan 0,362 en zero-shot sobre typed-decisions, con azar en 0,318. El 0,766 que se publica sale de un fine-tune sobre el split de train de ese mismo benchmark.
- **Se degrada con más de ~20 opciones** (Jev acepta 255). En Banking77 saca 0,425, contra 0,870 de Jev.
- **Para español, forzá el multilingual** (`default="multilingual"` o `lang_guess="es"`): la heurística de ruteo puede mandar textos cortos en español al checkpoint en inglés. El multilingual viene sin calibrar.
- **Los números de la landing no cierran**: "322M params, 650 MB" es sólo el multilingual, y "21 ms en M1 Max" contradice su propio JSON de benchmark, que da p50 de 45 ms.
- Juntó 18.9k stars en 5 días; no pudimos verificar si son orgánicas. Tiene bugs abiertos de calidad: `noul` sigue a las etiquetas en vez del contenido (#156) y hay sesgo de posición en `score` (#131).

**Licencia**: Apache-2.0 (código y pesos)
