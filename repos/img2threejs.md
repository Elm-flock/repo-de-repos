---
title: img2threejs
url: https://github.com/img2threejs/img2threejs
tags: [image-to-3d, threejs, skill, generative, typescript, apache-2.0]
added: 2026-08-11
added_by: Denis
---

Skill para coding agents que reconstruye el objeto de una imagen de referencia como modelo **Three.js procedural en TypeScript** (`THREE.Group` factory). No es fotogrametría ni mesh neural: es reconstrucción-por-código, quality-gated y listo para animar (pivots, sockets, colliders).

## Por qué vale la pena

- **Output versionable**: TypeScript + `ObjectSculptSpec` JSON diffable, no GLB de varios MB. Gallery live en [img2threejs-showcase](https://img2threejs.github.io/img2threejs-showcase/).
- **Pipeline por etapas con gates**: `blockout → structural → form → material → surface → lighting → interaction → optimization`; vision-review side-by-side hasta pasar umbrales. Fail-closed: `--strict-quality` bloquea specs superficiales antes de codegen.
- **Token-efficient de diseño**: scripts Python 3.10+ stdlib (cero pip) hacen validación/gating/estado; el modelo solo juzga visualmente y escribe el pass desbloqueado.
- **Sujetos**: hard-surface objects, characters (anatomía/proporciones), hybrids; opt-in likeness projection, multi-view visual hull, y review gates específicos CS2 (armas).
- **Multi-host**: Claude Code, Codex, OpenCode; agent-agnostic (vision nativa, browser MCP, preview o screenshot).
- **Límite honesto**: una sola imagen no revela lados ocultos; characters son estilizados, no likeness fotoreal. Distinto de TRELLIS.2 (mesh neural texturizado).

## Uso básico

```bash
git clone https://github.com/img2threejs/img2threejs.git ~/.claude/skills/img2threejs
# opcional: symlink a ~/.codex/skills/img2threejs
```

En el agent, adjuntar imagen y correr:

```text
/img2threejs Rebuild this object as a Three.js model, keep the proportions, angles, and colours.
```

Scripts standalone (sin deps): `python3 forge/stage1_intake/probe_image.py <image>`, etc. Estado multi-sesión: `forge/state.py` + `forge/next.py`.

**Licencia**: Apache 2.0
