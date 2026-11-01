# WebGPU Game of Life

Conway's Game of Life running entirely on the GPU with WebGPU, written while following Google's [Your first WebGPU app](https://codelabs.developers.google.com/your-first-webgpu-app) codelab.

> Archived: no longer maintained. Kept for reference.

## Credit

The structure and most of the code come from the Google codelab linked above. This repo is my working copy from going through it, not an original design.

## How it works

- A 64x64 grid is drawn on a 1024x1024 canvas as instanced squares, one instance per cell.
- Cell state lives in two storage buffers used in a ping-pong pattern: each step reads one and writes the other.
- A WGSL compute shader (8x8 workgroups) counts each cell's eight neighbours, wrapping at the edges, and applies the standard rules.
- A render pass then draws live cells, with the vertex and fragment shaders reading the same state buffer.
- The grid starts with random cells and updates on a fixed `setInterval` timer.

## Running

You need a browser with WebGPU enabled, such as recent Chrome or Edge. The page has to be served over HTTP rather than opened as a file:

```
npx serve .
# or
python3 -m http.server
```

Then open the printed local URL. `package.json` only holds `@webgpu/types` for editor type checking; there is no build step.

## Files

- `index.html`: canvas and script tag
- `script.js`: WebGPU setup, shaders, pipelines and the simulation loop

## Context

Written in December 2023 as an introduction to the WebGPU API and compute shaders.
