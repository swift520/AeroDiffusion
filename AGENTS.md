# Repository Guidelines

## Project Overview

This is a Vite + Vue 3 single-page academic project site for AeroDiffusion. The visible page is primarily implemented in `src/components/Main.vue`, with global app styling in `src/App.vue` and app setup in `src/main.js`.

## Common Commands

- Install dependencies: `npm install`
- Start local development server: `npm run dev`
- Build production output: `npm run build`
- Preview production build: `npm run preview`

There are no dedicated lint or test scripts configured in `package.json` at the moment. Use `npm run build` as the main verification step after code or asset path changes.

## Structure

- `src/components/Main.vue`: main page content, sections, text, video grids, and restart handlers.
- `src/App.vue`: Element Plus container/backtop and global typography/content styles.
- `src/main.js`: Vue app bootstrap and Element Plus registration.
- `src/assets/font/`: bundled Latin Modern font files and `font.css`.
- `public/`: static assets copied directly by Vite, including `total.png`, `favicon.svg`, and all `.mp4` files.
- `.github/workflows/ci.yml`: GitHub Pages deployment from `main` to `gh-pages` using Node 18 and `npm run build`.

## Development Notes

- This repo uses npm with `package-lock.json`; keep dependency changes in npm format.
- `vite.config.js` sets `base: '/AeroDiffusion'` for GitHub Pages. Update this only if the deployment path changes.
- Static files under `public/` are served from the site root in Vite. Existing video references use paths like `/video/traj_vis/1.mp4`.
- The media files in `public/` are large. Avoid renaming, recompressing, or replacing them unless the task explicitly calls for asset work.
- UI is built with Vue single-file components and Element Plus layout primitives. Prefer matching the existing simple academic-page style over introducing a new design system.
- Some inherited comments contain mojibake text. Preserve surrounding behavior when editing, and only clean comments if the task is specifically about readability or encoding.

## Verification

For most changes, run:

```sh
npm run build
```

When changing responsive layout, media paths, or autoplay behavior, also run the dev server and inspect the page in a browser.
