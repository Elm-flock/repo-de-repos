---
title: awesome-design-md
url: https://github.com/VoltAgent/awesome-design-md
tags: [design, frontend, coding-agent, directory, voltagent, mit]
added: 2026-09-25
added_by: Denis
---

Colección de `DESIGN.md` extraídos de sitios reales (Claude, Linear, Vercel, Stripe, Supabase, Notion, etc.) para copiar a la raíz del proyecto y que el agente de código genere UI con ese lenguaje visual en vez del look genérico de siempre. La mantiene VoltAgent, los del framework de agentes en TypeScript.

## Por qué vale la pena

- **Formato estándar, no inventado**: sigue la spec `DESIGN.md` de Google Stitch (el equivalente de `AGENTS.md` pero para cómo se ve el proyecto). Frontmatter YAML con tokens (colores con hex, familias tipográficas con fallbacks) más 9 secciones: tema visual, paleta con roles, tipografía, componentes con estados, layout, elevación, do/don't, responsive y una guía de prompts para el agente.
- **73 estilos, gratis y versionados en git**, bajo `design-md/<slug>/DESIGN.md`. Se pueden clonar, grepear o vendorizar sin cuenta. Categorías: plataformas de IA, dev tools, backend/DevOps, SaaS, fintech, e-commerce, medios, autos y una serie "Retro Web" de sitios de los '90.
- **CLI oficial `getdesign`** (npm, v0.6.25): `list` y `add <slug>`. Si ya hay un `DESIGN.md` en la raíz, guarda el nuevo en `<slug>/DESIGN.md` en vez de pisarlo.
- **Tracción**: ~118k estrellas y ~13k forks desde marzo de 2026, último push en septiembre de 2026.
- **Frente a [[refero-styles]]**: este es MIT, está en git y no tiene nada pago para el agente. Refero tiene muchos más estilos (dice "2,000+"), cinco formatos por estilo (Tailwind v4, CSS vars, tokens) y un MCP pago. [[hallmark]] cubre el caso de un sitio que no está en ninguna de las dos: genera un `design.md` desde una captura.

## Uso básico

```bash
npx getdesign list            # slugs disponibles
npx getdesign add linear.app  # escribe ./DESIGN.md (--force pisa, --out elige ruta)
```

Después: "leé `DESIGN.md` antes de escribir UI y respetá sus tokens, escala tipográfica y componentes".

**Trampas:**
- **Copiar el estilo de una marca puede traer problemas de marca registrada o trade dress.** Los archivos se presentan como "Inspired design analysis", no como el design system oficial.
- **Cuesta contexto**: el de Stripe pesa ~25 KB (varios miles de tokens) y se carga entero.
- **Los previews no están en el repo**: el `README.md` de cada carpeta redirige a getdesign.md, donde están el catálogo visual (claro/oscuro) y las descargas.
- **No aceptan PRs con estilos nuevos**, solo correcciones a los existentes. Para sumar un sitio hay que pedirlo en getdesign.md/request, que también ofrece pedidos privados. El README es a la vez vidriera de sponsors y starter kits pagos.

**Licencia**: MIT
