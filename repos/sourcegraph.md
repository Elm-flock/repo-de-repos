---
title: sourcegraph
url: https://sourcegraph.com
tags: [code-search, enterprise, saas, go]
added: 2026-08-21
added_by: Denis
---

Búsqueda y code intelligence sobre codebases multi-repo muy grandes, hoy reposicionado como infraestructura de contexto para agentes. **Ya no tiene versión gratis ni open source** — la duda que surgió en el canal ("¿ese me quiere cobrar?") tiene respuesta: sí.

## Por qué vale la pena guardarlo

Más como advertencia documentada que como recomendación. La historia de licencia importa porque hay mucha documentación y tutoriales viejos que asumen que es open source:

- **Oct-2018**: `sourcegraph/sourcegraph` se libera bajo Apache-2.0.
- **13-jun-2023**: último commit bajo Apache. Después pasa a la "Sourcegraph Enterprise License", propietaria.
- **Sep-2024**: el repo pasa a privado. `sourcegraph/sourcegraph-public-snapshot` es la copia pública **archivada** (último push 02-sep-2024). Su licencia prohíbe uso en producción: sólo permite copiar y modificar "for development and testing purposes".
- **Jul-2025**: se dan de baja Cody Free, Cody Pro y Enterprise Starter. `sourcegraph/cody` hoy da 404; queda `cody-public-snapshot` archivado.
- **Hoy**: un único plan Enterprise, "desde USD 16K", que escala con el tamaño del equipo. No hay tier self-serve gratis.

## Alternativa gratis, si lo que buscás es la búsqueda

**`sourcegraph/zoekt`** — el motor de búsqueda por trigramas que está debajo de Sourcegraph — sigue siendo **Apache-2.0, sin archivar y en desarrollo activo** (último push 20-ago-2026, ~1.8k stars, Go). Es la respuesta honesta a "quiero Sourcegraph pero gratis".

También queda libre la búsqueda pública sobre repos open source en `sourcegraph.com/search`.

Su herramienta de coding agéntico, **Amp**, se mudó a `ampcode.com` y tampoco es open source.

Relacionado: [[serena]] y [[codegraph]] resuelven la parte de dar contexto de código a un agente, self-hosted y con licencia permisiva.

**Licencia**: propietaria (Sourcegraph Enterprise License); el motor `zoekt` es Apache-2.0
