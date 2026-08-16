---
title: robotics-toolbox-python
url: https://github.com/petercorke/robotics-toolbox-python
tags: [robotics, python, kinematics, motion-planning, simulation]
added: 2026-08-16
added_by: Denis
---

Framework de robótica para Python: cinemática y dinámica de manipuladores serie, más de 50 modelos de robots reales (Franka-Emika, Kinova, UR, Rethink, Puma 560, etc.) y soporte para robots móviles (unicycle, bicycle, path planning con bug, D*, distance transform).

## Por qué vale la pena

- **Rápido de verdad**: cinemática directa y Jacobiano del manipulador en <1 µs, cinemática inversa numérica en ~4 µs.
- **Modelos listos para usar**: >50 robots comerciales y clásicos predefinidos, o los propios vía Denavit-Hartenberg o import de URDF.
- **Probalo sin instalar nada**: build a Wasm/Pyodide corriendo en JupyterLite directo desde el browser.
- Construido sobre `spatialmath-python` (del mismo autor) para el álgebra espacial (SO(3)/SE(3), quaternions, twists).
- Referencia estándar en investigación/educación de robótica en Python — 3.3k+ stars, mantenido por QUT Centre for Robotics.

## Uso básico

```bash
pip install roboticstoolbox-python
```

**Licencia**: MIT
