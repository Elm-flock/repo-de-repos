---
title: skill-recorder
url: https://github.com/microsoft/skill-recorder
tags: [skill, coding-agent, automation, typescript, microsoft, mit]
added: 2026-08-21
added_by: Emiliano
---

App de escritorio (Electron) que graba tu sesión de trabajo en pantalla y usa el CLI de GitHub Copilot para reconstruirla como intent + pasos ordenados, y de ahí generar una Skill (`SKILL.md`) o una Automation reutilizable para Microsoft Scout, Copilot Cowork o Copilot Studio.

## Por qué vale la pena

- **Invierte el flujo de escribir skills**: en vez de redactar el `SKILL.md` a mano, hacés la tarea una vez y el agente la generaliza a partir de ese ejemplo.
- **No graba video**: captura cambios de app/ventana activa, URLs del browser (sólo macOS), snapshots de pantalla a baja tasa disparados por cambio, y previews cortos de clipboard. Mucho menos pesado y menos invasivo que screen recording.
- **Narración transcrita on-device** con Whisper (99 idiomas, descarga única de ~252 MB). Durante la grabación nada sale de la máquina; sólo al apretar *Analyze* se sube el timeline + frames + texto a la nube de GitHub.
- **Prefiere herramientas nativas antes que replay de clicks**: los procedimientos generados usan `gh` CLI o `web_fetch` cuando puede, en vez de reproducir la UI — lo que hace la skill mucho más robusta.
- **Tracción rápida**: ~3.3k stars en las primeras dos semanas (repo creado el 29-jul-2026), release v0.5.0 del 12-ago-2026.
- Trae **eval suite** con fixtures (`npm run eval`, `npm run eval:builder`) para el describer y los builders.
- **Sin binarios**: sólo release por código fuente, y el instalador pinea un commit exacto de 40 caracteres (script + fuente). Nada se instala global.

## Uso básico

```bash
# macOS / Ubuntu — commit tomado de la página del último release
commit="<commit-de-40-chars>"
curl -fsSL "https://raw.githubusercontent.com/microsoft/skill-recorder/$commit/install.sh" \
  | SKILL_RECORDER_COMMIT="$commit" bash
```

```bash
npm ci && npm run dev   # desarrollo, requiere Node.js 24
```

Requiere cuenta de GitHub con acceso a Copilot (el CLI viene incluido) y permiso de Screen Recording en macOS. Windows 11 x64 y ARM64 soportados.

Relacionado: [[skillsmp]] para descubrir skills ya hechas; [[caveman]] y [[hallmark]] son skills que ya están en este repo.

**Licencia**: MIT
