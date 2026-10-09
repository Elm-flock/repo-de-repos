---
title: pen-dev
url: https://www.pen.dev
tags: [design, frontend, mcp, coding-agent, saas]
added: 2026-10-09
added_by: Emiliano
---

Canvas de diseño vectorial tipo Figma pensado para agentes (antes Pencil, `pencil.dev`). Funciona como app de escritorio, extensión de IDE y CLI headless, y expone un servidor MCP para que Claude Code, Codex o Cursor diseñen sobre archivos `.pen`. **Es closed source y hoy es gratis sólo porque los planes pagos todavía no arrancaron.**

## Por qué vale la pena

- **Formato `.pen` abierto**: JSON con el schema publicado. Importa `.fig` de Figma, HTML y páginas web; exporta HTML/CSS/Tailwind, PNG, JPEG, WEBP y PDF.
- **El agente diseña desde el IDE**: herramientas MCP `get_style`, `read_skill`, `get_app_state` y `execute`. Extensión para VS Code, Cursor, Windsurf y Antigravity (1,47M descargas en Open VSX).
- **CLI para CI**: `@pen.dev/cli` genera diseños por prompt y exporta, con una clave de organización en `PEN_CLI_KEY`.
- **Multiplataforma**: app v1.2.16 (8-oct-2026) para macOS, Windows y Linux, x64 y arm64.
- **Precios anunciados**: Free con 5 "agent days" por mes, Pro USD 16 y Ultra USD 48 por usuario/mes, con el toggle anual activado; el precio mensual no lo verificamos.
- Comunidad: skills de diseño para Claude Code (`stevembarclay/pencilplaybook`, `Nisus74/pencil-skill`) y sync bidireccional diseño↔código (`artificemachine/pencil-sync`).

## Uso básico

```bash
npm install -g @pen.dev/cli
pen login
pen --out design.pen --prompt "Create a login page"
pen --in design.pen --export design.png
```

App de escritorio: <https://www.pen.dev/downloads>. El MCP sólo funciona con la app o el IDE abiertos y un `.pen` cargado. El CLI y el agente requieren cuenta.

Relacionado: [[kombai]] (canvas + código para frontend) y [[refero-styles]] (DESIGN.md de sitios reales para darle estilo al agente).

**Licencia**: propietaria (EULA de High Agency, Inc.); el CLI figura como `UNLICENSED` en npm
