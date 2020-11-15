## Developing in this monorepo

There are a few directories in this monorepo:

- [`box2d`](https://github.com/erincatto/box2d)
  - This is a git submodule of the [`box2d`](https://github.com/erincatto/box2d) C++ source code.
- **[`box2d-wasm`](box2d-wasm)**
  - Compiles [`box2d`](https://github.com/erincatto/box2d) to WebAssembly
    - Compiled using [Emscripten](https://emscripten.org/index.html) toolchain
  - Creates `.js` bindings to WebAssembly functionality
    - Exported functionality is described as `.idl` WebIDL bindings
    - Bindings emitted via [WebIDL binder](https://emscripten.org/docs/porting/connecting_cpp_and_javascript/WebIDL-Binder.html)
  - Creates `.d.ts` declarations for `.js` bindings
    - Declarations generated by [`webidl-to-ts`](webidl-to-ts)
- [`webidl-to-ts`](webidl-to-ts)
  - Generates TypeScript `.d.ts` declarations from `.idl` [WebIDL bindings](https://emscripten.org/docs/porting/connecting_cpp_and_javascript/WebIDL-Binder.html) files.
    - `.idl` file parsed using W3C's [WebIDL parser](https://github.com/w3c/webidl2.js/)
    - TypeScript declarations created with TypeScript Compiler API
- [`integration-test`](integration-test)
  - For testing changes you've developed to [`box2d-wasm`](box2d-wasm)
  - Svelte application that demonstrates how to consume [`box2d-wasm`](box2d-wasm) via TypeScript
- [`demo`](demo)
  - Examples of how to integrate `box2d-wasm` into your application

### Clone repository

Clone this repository using --recursive, to ensure that the [`box2d`](https://github.com/erincatto/box2d) submodule is available.  
_Tutorial: [Using submodules in Git](https://www.vogella.com/tutorials/GitSubmodules/article.html)_

```bash
# start in root of repository
git clone --recursive git@github.com:Birch-san/box2d-wasm.git
cd box2d-wasm
```

#### Instantiate packages

[`pnpm`](https://pnpm.js.org/) is used to manage packages in this monorepo. In particular, it creates a symlink that enables `integration-test` to consume build artifacts from `box2d-wasm`.

```bash
# from root of repository
npm i -g pnpm
pnpm i
# compile webidl-to-ts from TS to JS, so that box2d-wasm can consume it to generate typings
pnpm build --filter=webidl-to-ts
```

### Compile Box2D to WASM + generate .js and .d.ts bindings

See README of [`box2d-wasm`](box2d-wasm) package.

### Test `box2d-wasm` functionality inside an application

See README of [`integration-test`](integration-test) package.