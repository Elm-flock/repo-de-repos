---
title: newman
url: https://github.com/postmanlabs/newman
tags: [cli, api-testing, ci-cd, nodejs, apache-2.0]
added: 2026-07-30
added_by: Emiliano
---

Collection runner de Postman por línea de comandos (Node.js). Ejecuta y testea colecciones de Postman desde la terminal, sin la GUI. No es IA, pero es tooling de terminal que suma.

## Por qué vale la pena

- **Pensado para CI/CD**: se integra con servidores de integración continua y build systems para automatizar tests de API.
- **Testing data-driven** por iteraciones (archivos de datos), con soporte de environments y variables globales.
- **Reporters integrados**: CLI, JSON, JUnit (XML para CI) y progress; HTML como reporter externo (se instala aparte).
- **Extras**: certificados SSL/cliente, configuración de proxy, subida de archivos y compatibilidad con Docker.
- Newman v6.x requiere Node.js 16+.

## Uso básico

```bash
npm install -g newman   # alternativa macOS: brew install newman
newman run coleccion.json
```

**Licencia**: Apache 2.0
