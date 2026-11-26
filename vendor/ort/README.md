# ONNX Runtime Web 1.30.0（MIT，Microsoft）

从 MulTape 的 `v2/node_modules/onnxruntime-web/dist/`（npm 包 onnxruntime-web 1.30.0）原样复制，没有改动。
许可证：`../../LICENSES/onnxruntime-web/LICENSE`。

| 文件 | 大小 | 用途 |
|---|---|---|
| `ort.wasm.bundle.min.mjs` | 73 KB | 只含 WebAssembly 后端的 ES 模块（自带 Emscripten 胶水代码）。`voice.worker.js` 第一次要说话时才 `import()` 它。 |
| `ort-wasm-simd-threaded.wasm` | 14.2 MB | 运行时本体。**不在打开页面时下载**：作为语音包的一部分下载、核对 SHA-256、存进 Cache Storage（`voice-pack/` 下面只存一份，Supertonic 和中文的 Melo 两个包共用），再交给 `env.wasm.wasmBinary`；第一个模型打开后就放掉这份字节（运行时已经初始化好了）。 |
| `ort-wasm-simd-threaded.mjs` | 24 KB | 只在多线程时用（页面 cross-origin isolated 时），线程从它启动（`env.wasm.wasmPaths.mjs`）。单线程时不会被加载。 |

`ort.wasm.bundle.min.mjs` 末尾指向一个 `.map` 文件，没有复制（只是开发者工具里会有一条 404，不影响使用）。

升级 ONNX Runtime 时：三个文件一起换，并更新 `voice.js` 清单里 wasm 的大小、SHA-256 和分段哈希（`WASM`），以及两个包的版本（`VERSION` 和 Melo 的 `version`），这样已经装过的人会重新下。
