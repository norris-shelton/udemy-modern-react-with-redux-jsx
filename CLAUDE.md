# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

This is the React Starter Project for Stephen Grider's "Modern React with Redux" Udemy course. It is currently the unmodified Create React App-style boilerplate scaffolded on top of Vite.

## Commands

- `npm start` — start the Vite dev server on http://localhost:3000 (port is fixed in `vite.config.js`)
- `npm run build` — production build to `dist/`
- `npm run preview` — serve the production build locally
- `npm run lint` — run ESLint over the repo

There is no test runner configured.

## Architecture

- **JSX in `.js` files.** This project writes JSX inside `.js` files (not `.jsx`). Vite does not do this by default, so `vite.config.js` adds a custom `treat-js-files-as-jsx` plugin that runs esbuild's JSX loader over any `src/**/*.js` file, plus an `optimizeDeps` esbuild override. When adding source files, use `.js` — `.jsx` is unnecessary and the rest of the codebase uses `.js`.
- **Entry chain:** `index.html` loads `src/index.js`, which mounts `<App />` (from `src/App.js`) into `#root` via React 19's `createRoot`, wrapped in `<StrictMode>`.
- **Root-level `index.js`** is an unused leftover (`console.log('Happy developing ✨')`) — not part of the app. The real entry point is `src/index.js`.
- React 19 with the automatic JSX runtime (no `import React` needed in components).

## ESLint note

The ESLint config (`eslint.config.js`) is flat-config and pins `settings.react.version` to `18.3` even though the dependency is React 19. It also disables `no-unused-vars` and `react/prop-types`.
