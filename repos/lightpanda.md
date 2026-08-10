---
title: lightpanda
url: https://github.com/lightpanda-io/browser
tags: [browser, automation, agents, cli, zig, agpl-3.0]
added: 2026-08-10
added_by: Emiliano
---

Browser headless escrito desde cero en Zig, pensado para agentes de IA y automatización. No es un fork de Chromium ni un patch de WebKit: al no arrastrar la capa de rendering ni la UI, el consumo de memoria y el tiempo de ejecución bajan un orden de magnitud frente a headless Chrome.

## Por qué vale la pena

- **Benchmark propio** (933 páginas reales sobre EC2 m5.large, 100 páginas): 123MB de memoria pico vs 2GB de headless Chrome (~16× menos) y 5s vs 46s de ejecución (~9× más rápido).
- **Habla CDP**, así que se enchufa a Puppeteer / Playwright sin cambiar el código del cliente.
- **`--dump markdown` nativo**: convierte la página directo a markdown para meterla en un contexto de LLM, con `--wait-until`, `--wait-ms`, `--wait-selector` y `--wait-script` para controlar la espera.
- **`--obey-robots`** incorporado en el `fetch`.
- Distribución simple: nightly binaries para Linux/macOS (x86_64 y aarch64), Homebrew, AUR e imágenes Docker oficiales.

## Uso básico

```bash
brew install lightpanda-io/browser/lightpanda
# o Docker con el server CDP en 9222:
docker run -d --name lightpanda -p 127.0.0.1:9222:9222 lightpanda/browser:nightly

lightpanda fetch --obey-robots --dump markdown https://example.com
```

Sin binario nativo de Windows (va por WSL2; WSL forwardea `localhost:9222` solo). Los binarios de Linux linkean contra glibc: en distros musl (Alpine) hay que compilar o usar base image glibc.

**Licencia**: AGPL 3.0
