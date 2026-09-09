<!-- agents-md ceiling: 51 lines -->
# AGENTS.md — mgr-pdf-viewer-react

A published npm React component: a simple PDF viewer with controls.

## This project is not maintained

[`README.md`](README.md) opens with a deprecation notice, and it is the first thing to
believe: the project is not maintained, `react-pdf` is the named alternative, and mgrin has
offered to hand ownership over. **Do not start feature work here.** What is still worth
doing, and all that has been done recently, is small and defensive: a bug that breaks real
consumers, a packaging fix, a release.

## Commands, all run 2026-09-09

```sh
npm install       # rc=0
npm run build     # rollup-babel-lib-bundler src/index.js -> dist/, rc=0, ~160ms
```

**There is no test suite and no CI.** `.github/` does not exist and `npm test` is not
defined, so the build succeeding is the only automatic signal there is. Verify a change
against `example/`, in a browser, and say so in the PR.

## Layout

| path | what it is |
|---|---|
| `src/` | the component source — the only input to the build |
| `dist/`, `index.js` | build output, **committed**, and shipped: they are in `files` |
| `example/` | the demo, and the only way to see a change work |
| `.babelrc`, `.eslintrc` | the toolchain config; the bundler is rollup via `rollup-babel-lib-bundler` |

## Conventions that differ from the defaults

- **`react`, `prop-types` and `react-pdf-js` are externals**, resolved from the consumer's
  tree. The build prints "Treating X as external dependency" for each; a new import that
  does not appear there has been bundled in, which is a packaging bug.
- **`react` is a peer dependency at `>=15.3.2`.** That range is the compatibility promise
  and narrowing it is a breaking release.
- **`files` is an allowlist** — `dist`, `src`, `index.js`, `README.md`, `LICENSE`. It was
  added so `example/` stopped shipping to npm; a new top-level asset that must ship has to
  be added there or it silently will not.
- **`dist/` is committed**, unusually. Rebuild and commit it with the source change, or the
  published artifact and the source disagree.

**Nothing about who may merge, how agents are spawned, or how the maintainer's
machine handles secrets belongs in this file, and none of it is stated here.**
Those are properties of a working environment, not of this project; if you are
contributing, your own conventions apply and nothing in this repo depends on
the maintainer's.
