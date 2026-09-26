---
title: refero-styles
url: https://styles.refero.design
tags: [design, frontend, coding-agent, saas]
added: 2026-09-23
added_by: Francisco
---

Biblioteca de `DESIGN.md` extraídos de sitios reales (ElevenLabs, Brex, Linear, Vercel, etc.) para pegar en el contexto de un agente de código y que adopte ese look and feel. Buscás el estilo, lo copiás y lo pegás. La hace Refero, los de la biblioteca de UI refero.design. **Está en beta y el MCP es pago.**

## Por qué vale la pena

- **Resuelve el "todo se ve igual" de la UI generada por LLM** con un estilo concreto como referencia, en vez de reglas genéricas.
- **Cinco formatos por estilo**: Preview, `DESIGN.md`, Tailwind v4, CSS Variables y Design Tokens. Cada uno trae paleta con roles, escala tipográfica con fuentes y fallbacks, spacing, radios, elevación, do/don't y componentes.
- **Copiar es gratis**, sin cuenta. La home habla de "2,000+" estilos con altas semanales; no lo contamos.
- Tiene skill oficial: `referodesign/refero_skill` (MIT).
- Con plan pago (Pro, Team o Lifetime) hay un MCP (`https://api.refero.design/mcp`) para que el agente busque estilos solo. El plan Free no lo incluye y no hay trial.

## Uso básico

Copiar a mano desde <https://styles.refero.design>, o instalar la skill:

```bash
npx skills add https://github.com/referodesign/refero_skill --skill refero-design
# con plan pago:
claude mcp add --transport http refero https://api.refero.design/mcp --header "Authorization: Bearer <token>"
```

**Trampas:**
- **Copiar tal cual el estilo de una marca puede traer problemas de marca registrada o trade dress.** La propia doc dice "Styles are guidance, not templates".
- Los términos permiten uso comercial en trabajo de diseño, pero **prohíben redistribuir, hacer scraping y usarlo para entrenar modelos**. Los MCP no oficiales de la comunidad hacen scraping, así que probablemente violan esos términos.
- Los precios de los planes no se pudieron verificar: la página los renderiza con JS.

Relacionado: [[awesome-design-md]] es la alternativa MIT y en git, con menos estilos (73), [[hallmark]] ataca el mismo problema con reglas anti-slop y puede generar un `design.md` a partir de una captura, [[kombai]] es un agente de frontend completo, y [[skillsmp]] es el directorio de skills.

**Licencia**: contenido propietario (términos de uso de Refero); la skill oficial es MIT
