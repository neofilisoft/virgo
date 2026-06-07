# Virgo Engine

> Browser-first game engine targeting **WebGPU + WebAssembly**  
> © **Neofilisoft / Studio Balmung**

---

## Feature Set

| Feature | Implementation |
|---------|---------------|
| 2D Rendering | PixiJS 8 - WebGPU → WebGL auto-select |
| 3D Rendering | Native WebGPU, PBR WGSL shader |
| Mesh Optimization | meshoptimizer - 4-level auto-LOD |
| Entity Component System | bitecs - 100k entities, SoA cache-friendly |
| 3D Spatial Audio | Google Resonance Audio (HRTF) |
| Music / Synthesis | Tone.js - BPM transport, samplers, effects |
| Pathfinding | Pathfinding.js - A* on navmesh grid |
| Input | Keyboard + Pointer + Gamepad, action map |
| Scripting | TypeScript Behaviours + Event Sheets + Node Graph |
| Networking | Client-side prediction stub (WebSocket) |
| Asset Pipeline | CLI (prod) + Vite plugin (dev hot-reload) |
| Editor | VS Code extension - Inspector + Node Graph |

---

## Packages

```
packages/
  core             Engine, EventBus, GameLoop, PluginRegistry, SceneManager
  ecs              bitecs World, built-in components, SystemScheduler
  renderer-2d      PixiJS 8 plugin, Camera2D, ECS sprite sync
  renderer-3d      WebGPU pipeline, PBR shader, MeshRegistry (LOD)
  audio            Resonance Audio + Tone.js plugin
  input            Unified input + action binding
  physics          AABB collisions + Pathfinding.js navmesh
  scripting        TS Behaviours, Event Sheets, Node Graph
  networking       Client-side prediction, snapshot interpolation
  asset-pipeline   CLI build + Vite hot-reload plugin
  editor-bridge    Comlink DevTools protocol
  runtime          Single-import facade (start here)

tools/
  cli              virgo init | build | export | serve
  vscode-extension Scene Inspector + Node Graph WebViews
```

---

## Quick Start

```bash
npm install -g @virgo/cli
virgo init my-game
cd my-game && npm install
virgo serve
```

```ts
// src/main.ts
import { VirgoEngine } from "@virgo/runtime";

const engine = await VirgoEngine.create({
  canvas: document.getElementById("canvas") as HTMLCanvasElement,
  mode: "2d",               // "2d" | "3d" | "dual"
});

engine.scenes.register("main", () => import("./scenes/MainScene.js"));
await engine.loadScene("main");
engine.start();
```

---

## Engine Modes

| Mode | Renderers loaded |
|------|-----------------|
| `"2d"` | PixiJS only |
| `"3d"` | WebGPU pipeline only |
| `"dual"` | Both - 3D world + 2D overlay |

---

## VS Code Extension

Install from `tools/vscode-extension/`. Provides:
- **Scene Inspector** - live entity tree, ECS component values, pause/step/reload
- **Node Graph Editor** - drag-and-drop visual scripting, exports `NodeGraph` JSON
- **Auto hot-reload** on file save
- **Asset Build** task

---

## WebGPU Requirements

WebGPU requires:
- Chrome 121+ / Edge 121+ / Firefox Nightly
- HTTPS in production
- `Cross-Origin-Opener-Policy: same-origin`
- `Cross-Origin-Embedder-Policy: require-corp`

The scaffolded `vite.config.ts` sets these headers automatically in dev.

---

## Documentation

See [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) for the full reference.

---

*2026 © by Neofilisoft / Studio Balmung*
