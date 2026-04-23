# IMPLEMENTATION_PHASE1.md

## Phase 1: Static App Scaffold and NPM Validation Baseline

This phase establishes the project foundation for the PXL Sweeper browser game by creating a runnable static web app scaffold and a reproducible npm workflow.

---

## 1. Architectural Design

### Goals for this phase
- Provide a minimal static entry point for the web app.
- Provide a reproducible `npm` workflow with `test`, `lint`, and `build` hooks.
- Create the first app bootstrap module and stylesheet.

### Data structures and state definitions

The app is intentionally minimal in Phase 1. Define the following shape as the early scaffold state to support later game work:

```js
// src/index.js
export const defaultAppState = {
  isReady: false,
  phase: 1,
  message: 'PXL Sweeper scaffold loaded',
  boardConfig: {
    rows: 8,
    cols: 8,
    mines: 10,
  },
};
```

### Function signatures

The entrypoint module should expose bootstrap functions and a render stub for future expansion.

```js
export function initApp(containerSelector = '#app')
  -> void

function createAppRoot(containerSelector: string)
  -> HTMLElement

function renderPlaceholder(root: HTMLElement, state: typeof defaultAppState)
  -> void

function attachAppStylesheet()
  -> void
```

### Runtime contract

- `index.html` loads `src/index.js` as an ES module.
- `src/index.js` mounts into the DOM element with `id="app"`.
- `src/styles.css` is loaded by `index.html` and applies a clean base layout.

---

## 2. File-Level Strategy

Exact files to touch in this phase:

- `package.json`
  - Define `scripts`: `test`, `lint`, and `build`.
  - Include `devDependencies` for baseline tooling.
  - Optionally set `type: "module"` if using ES module imports.
- `index.html`
  - Provide document structure, root container, stylesheet link, and module script import.
- `src/index.js`
  - Implement the app bootstrap and placeholder render.
- `src/styles.css`
  - Add page-level reset and app scaffolding styles.
- `tests/app.test.js`
  - Add a minimal smoke test to validate the test harness.
- `.gitignore`
  - Ignore `node_modules/` and output directories such as `dist/`.
- `TODO.md`
  - Refresh the file with the next phase tasks from `IMPLEMENTATION_PLAN.md`.

> Do not implement game logic in this phase. Keep only the static scaffold and workflow baseline.

---

## 3. Atomic Execution Steps

### [ ] Create `package.json` with npm scripts for test, lint, and build.

- Plan
  - Choose a minimal toolchain: `eslint` for lint, `jest` for smoke tests, and a simple static build script.
  - Define `package.json` fields: `name`, `version`, `private`, `type`, `scripts`, `devDependencies`.
  - Add `.gitignore` to prevent committing dependencies or build artifacts.
- Act
  - Create `package.json` with exact script definitions.
  - Add `devDependencies` for tooling.
  - Add `.gitignore` with at least `node_modules/` and `dist/`.
- Validate
  - Run `npm install` successfully.
  - Run `npm test` and verify it exits with success.
  - Run `npm run lint` and verify it exits with success.
  - Run `npm run build` and verify it exits with success.

### [ ] Add `index.html`, base stylesheet, and app entrypoint file.

- Plan
  - Create the static page structure with a root container `#app`.
  - Import `src/index.js` using `type="module"`.
  - Add a base stylesheet to visually confirm the app loaded.
  - Implement `src/index.js` to render a placeholder message and set `isReady: true`.
- Act
  - Create `index.html`, `src/index.js`, and `src/styles.css`.
  - Ensure the script path and stylesheet path are correct relative to `index.html`.
  - Add a placeholder DOM state so the page is not blank.
- Validate
  - Open `index.html` in a browser or preview and verify the placeholder appears.
  - Confirm no console errors from loading `src/index.js`.
  - Confirm the stylesheet is applied.

### [ ] Verify the app scaffold loads in a browser or local preview.

- Plan
  - Use the browser or a static preview server to load the page.
  - Confirm the placeholder content and app container are present.
- Act
  - Launch the preview via a local server or open the file directly.
  - Inspect the DOM and console.
- Validate
  - The page displays a clear scaffold message.
  - The `#app` container exists and contains rendered content.
  - No JS load or network errors appear.

---

## 4. Edge Case & Boundary Audit

Specific failure modes and boundary conditions for Phase 1:

- `package.json` missing one of the required scripts or using invalid command syntax.
- `index.html` references `src/index.js` with the wrong relative path.
- `src/index.js` fails to execute because the browser rejects unsupported syntax or missing `type="module"`.
- `src/styles.css` is not loaded due to an incorrect href.
- `npm run lint` fails because tooling is configured incorrectly or file paths are wrong.
- `npm run build` fails because `build` uses an absent tool or invalid command.
- The app root container ID does not exist, causing mount failure.
- The local preview loads the file but does not render because `window.onload` / module execution is never invoked.
- A missing `tests` folder means `npm test` has no valid entry point.

Boundary conditions to explicitly handle:

- The repository may be empty; all required directories should be created.
- The browser should not require advanced build output to display the initial scaffold.
- The static scaffold must work in a plain file preview as well as an npm-driven build.

---

## 5. Verification Protocol

### Manual UX checklist

- [ ] Open `index.html` and confirm the page title is `PXL Sweeper`.
- [ ] Confirm the visible placeholder content is rendered inside `#app`.
- [ ] Confirm `src/styles.css` is applied to the page.
- [ ] Confirm the browser console has no script load or runtime errors.
- [ ] Confirm the app root container remains present after page load.

### Automated validation checklist

- [ ] `npm install` completes without errors.
- [ ] `npm test` exits successfully.
- [ ] `npm run lint` exits successfully.
- [ ] `npm run build` exits successfully.
- [ ] `package.json` contains `test`, `lint`, and `build` scripts.
- [ ] `TODO.md` is updated with Phase 2 tasks from `IMPLEMENTATION_PLAN.md`.

### Minimal baseline test cases

- `tests/app.test.js` should validate that the app module can be imported and that default state exists.
- Optionally verify `defaultAppState.isReady` is `false` before bootstrap.

---

## 6. Code Scaffolding

### `package.json` skeleton

```json
{
  "name": "pxl-sweeper",
  "version": "0.1.0",
  "private": true,
  "type": "module",
  "scripts": {
    "test": "jest",
    "lint": "eslint . --ext .js",
    "build": "mkdir -p dist && cp index.html dist/index.html && cp -r src dist/src"
  },
  "devDependencies": {
    "eslint": "^8.0.0",
    "jest": "^29.0.0"
  }
}
```

### `index.html` skeleton

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>PXL Sweeper</title>
    <link rel="stylesheet" href="src/styles.css" />
  </head>
  <body>
    <main id="app" class="app-root"></main>
    <script type="module" src="src/index.js"></script>
  </body>
</html>
```

### `src/index.js` skeleton

```js
export const defaultAppState = {
  isReady: false,
  phase: 1,
  message: 'PXL Sweeper scaffold loaded',
  boardConfig: {
    rows: 8,
    cols: 8,
    mines: 10,
  },
};

export function initApp(containerSelector = '#app') {
  const root = createAppRoot(containerSelector);
  renderPlaceholder(root, defaultAppState);
}

function createAppRoot(containerSelector) {
  const root = document.querySelector(containerSelector);
  if (!root) {
    throw new Error(`App root not found: ${containerSelector}`);
  }
  return root;
}

function renderPlaceholder(root, state) {
  root.innerHTML = `
    <section class="app-placeholder">
      <h1>PXL Sweeper</h1>
      <p>${state.message}</p>
      <pre>${JSON.stringify(state.boardConfig, null, 2)}</pre>
    </section>
  `;
}

initApp();
```

### `src/styles.css` skeleton

```css
:root {
  font-family: system-ui, sans-serif;
  line-height: 1.5;
  color: #111;
  background: #f8f8fb;
}

* {
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  min-height: 100vh;
}

body {
  display: grid;
  place-items: center;
  padding: 1rem;
}

.app-root {
  width: min(600px, 100%);
  background: #ffffff;
  border: 1px solid #d7d7e0;
  border-radius: 16px;
  padding: 1.5rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
}

.app-placeholder h1 {
  margin-top: 0;
}
```

### `tests/app.test.js` skeleton

```js
import { defaultAppState } from '../src/index.js';

describe('PXL Sweeper scaffold', () => {
  test('default app state is defined', () => {
    expect(defaultAppState).toBeDefined();
    expect(defaultAppState.phase).toBe(1);
    expect(defaultAppState.boardConfig.rows).toBe(8);
  });
});
```

### `.gitignore` skeleton

```
node_modules/
dist/
```

---

## Summary

This blueprint keeps Phase 1 narrowly focused on establishing the static entrypoint, the npm validation baseline, and a clean scaffold for later game logic.

Do not implement game mechanics or UI interactions in this phase. Create only the files listed above and confirm all baseline commands and preview checks succeed before moving to Phase 2.
