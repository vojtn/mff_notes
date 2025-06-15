# Javascript
---

## Task Runner

automates repetitive development tasks such as:
- Minifying CSS/JS
- Compiling preprocessor code (like SASS)
- Linting
- Watching files for changes

**Examples:** `Gulp`, `Grunt`

Task runners are often script-based and configurable using JavaScript.

---

## Bundler

takes application's source files (JavaScript, CSS, images, etc.) and **combines them into optimized bundles** (usually fewer files) to:
- Reduce HTTP requests
- Optimize performance
- Support module systems (CommonJS, ESModules)

**Examples:** `Webpack`, `Parcel`, `Rollup`, `Vite`

---

## Gulp.js

- A **task runner** written in JavaScript, based on Node.js streams.
- Uses `gulpfile.js` to define tasks like:
  - Minification
  - Compilation
  - File watching
- Offers **manual control** over build steps.
- Focuses on **orchestration of tasks**, not bundling.

---

## Webpack

- A **powerful module bundler**.
- Handles:
  - JavaScript modules (ESM/CommonJS)
  - CSS, images, fonts via loaders
  - Code splitting and lazy loading
- Supports **plugins and loaders** for customization.
- Can also perform tasks that Gulp does (minification, transpilation).
- Often used with frameworks like React, Vue, Angular.

---

## Parcel.js

- A **zero-config bundler** for web apps.
- Automatically detects and bundles assets (JS, CSS, HTML, images).
- Simpler to configure than Webpack.
- Supports hot module replacement (HMR).
- Ideal for small to medium projects.

---

## Vite

- A **modern bundler and dev server** created by Evan You (Vue.js author).
- Uses **native ES Modules** in development for fast startup.
- Bundles using **Rollup** in production.
- Very fast and developer-friendly.
- Works with Vue, React, Svelte, and other frameworks.
- Supports HMR, TypeScript, JSX out-of-the-box.

---

## SSR (Server-Side Rendering)

- Rendering HTML content **on the server** instead of in the browser.
- Benefits:
  - Faster time-to-content
  - Better SEO
  - Performance on slower devices
- Common in:
  - **Next.js** (React)
  - **Nuxt.js** (Vue)
  - **SvelteKit**
- Can be combined with hydration to turn static pages into dynamic ones after load.

---