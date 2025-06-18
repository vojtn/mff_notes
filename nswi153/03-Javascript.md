[Back to overview](/Readme.md)


# Javascript

## CSS libraries
### Bootstrap
- One of the most popular CSS frameworks.
- Provides a **12-column grid system**, UI components (buttons, navbars, forms), and responsive design utilities.
- Originally built by Twitter.
- Includes optional support for **SASS**.
- Helps create consistent UIs quickly.

---

### Material Design
- **Design system** created by Google.
- Aims for clean, consistent UI across platforms.
- Defines spacing, typography, components, etc.
- Implemented in libraries such as:
  - **Material UI (MUI)** for React
  - **Angular Material**
  - **Materialize CSS**
---

### Tailwind CSS
- **Utility-first CSS framework**.
- Encourages using utility classes in HTML (e.g., `p-4`, `text-center`) instead of writing custom CSS.
- Promotes consistency and eliminates unused styles (via PurgeCSS).
- Good for scalable design systems.
- No default UI components.

---

## CSS Preprocessors

Allow you to write CSS with extended syntax and compile it into standard CSS.

### Benefits:
- Code reusability
- Nesting for better structure
- Variables and functions
- Easier maintenance for large stylesheets

---

### SASS (Syntactically Awesome Stylesheets)
- Most widely used preprocessor.
- Features:
  - Variables (`$color: red`)
  - Nesting
  - Mixins (reusable chunks)
  - Functions
  - Partials and imports

---

### LESS
- Another CSS preprocessor.
- Created by the Bootstrap team originally.
- Simpler syntax than SASS.
- Uses JavaScript-based logic (functions, operations).

---

## Javascript runtimes

### Node.js
- JavaScript runtime built on **V8 engine** (used in Chrome).
- Designed for **server-side applications**.
- Uses **asynchronous, event-driven architecture**.
- Has built-in modules like `fs`, `http`, `net`, etc.
- Package manager: **npm**

---

### Deno
- A secure JavaScript and TypeScript runtime.
- Created by **Node.js's original author (Ryan Dahl)**.
- Features:
  - Native TypeScript support
  - Built-in linter, formatter
  - Secure by default (sandboxed environment)
  - Uses **ES Modules** (`import`)

---

### Bun
- Very fast modern JavaScript runtime, bundler, test runner, and package manager.
- Written in **Zig**.
- Targets performance and developer productivity.
- Native support for many Node APIs.
- Still **experimental** on Windows (as of mid-2025).

---

## TypeScript
- A **typed superset of JavaScript**.
- Developed by **Microsoft**.
- Adds:
  - Static typing
  - Interfaces and types
  - Compile-time checking
- Compiles to plain JavaScript.
- Improves code maintainability and tooling (auto-completion, refactoring).

---

## ELM
- A **purely functional** programming language for building **web frontends**.
- Compiles to JavaScript.
- Features:
  - Strong static typing
  - No runtime exceptions
  - Immutability by default
- Emphasizes **reliability and maintainability**.

---
[Back to overview](/Readme.md)
