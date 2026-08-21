---
title: litert-js
url: https://github.com/google-ai-edge/LiteRT/tree/main/litert/js
tags: [inference, on-device, browser, webgpu, typescript, apache-2.0]
added: 2026-08-21
added_by: Emiliano
---

Runtime de Google para correr modelos LiteRT (`.tflite`) directamente en el browser, con aceleración WebGPU o CPU vía XNNPACK. Reemplaza `loadGraphModel` en pipelines existentes de TensorFlow.js.

## Por qué vale la pena

- **No tiene repo propio**: vive en el subdirectorio `litert/js` del monorepo `google-ai-edge/LiteRT`. Vale saberlo antes de buscar `LiteRT.js` como repo suelto (da 404).
- **Performance reportada por Google** (MacBook Pro M4, 09-jul-2026): hasta **3× más rápido que otros runtimes web** en CPU y GPU, y **5–60×** de speedup GPU/NPU contra ejecución en CPU pura. Números self-reported.
- **Tres backends**: XNNPACK multi-thread en CPU (funciona en cualquier browser), ML Drift sobre WebGPU para GPU, y WebNN/NPU experimental en Chrome y Edge (aprovecha CoreML en Apple).
- **Convierte desde PyTorch, JAX o TensorFlow** — desde PyTorch en un solo paso con `google-ai-edge/litert-torch`. AI Edge Quantizer permite esquemas de cuantización por capa.
- **Integraciones reales**: Ultralytics tiene export oficial a LiteRT para YOLO; hay colección "LiteRT Community" en HuggingFace y modelos en Kaggle. Proyecto hermano `LiteRT-LM` para LLMs on-device.

## Uso básico

```bash
npm i @litertjs/core @litertjs/tfjs-interop
```

```typescript
import {loadLiteRt, loadAndCompile} from '@litertjs/core';
await loadLiteRt('your/path/to/wasm');
const model = await loadAndCompile('/mobilenet_v2.tflite', {accelerator: 'webgpu'});
```

**Límites duros que conviene saber antes de adoptarlo**:
- La memoria de WebAssembly topea en **2 GB**, así que modelos grandes pueden no cargar.
- En browsers **con JSPI** los ops no soportados por WebGPU delegan a WASM op por op; en browsers **sin JSPI** un solo op no soportado tira **todo el modelo** a CPU por el límite síncrono.
- **No hace pre/post-processing**: eso lo pones vos o TFJS. Para pipelines end-to-end, Google recomienda MediaPipe Web Solutions.
- Manejo manual de memoria: los tensores requieren `.delete()` explícito.

Los packages npm (`@litertjs/core` 2.5.3) versionan aparte de los tags del repo C++ (v2.2.0).

Relacionado: [[utopiaia-translator]], otro caso de inferencia on-device en el browser con WebGPU.

**Licencia**: Apache-2.0
