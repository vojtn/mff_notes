## jQuery

- Released in **January 2006**.
- A **JavaScript library** that simplifies DOM manipulation, event handling, animation, and AJAX.
- Known for its **`$()` selector syntax**.
- Abstracts away browser inconsistencies.
- Was extremely popular before modern frameworks (React, Angular, Vue).
- Supports **AJAX** with simplified syntax: `$.get()`, `$.ajax()`, etc.
- **Nowadays:** Considered legacy; rarely used in modern apps.

---

## Angular

- A **TypeScript-based frontend framework** developed by **Google**.
- Complete solution: includes routing, forms, HTTP client, etc.
- Uses:
  - **Components**
  - **Modules**
  - **Two-way data binding**
  - **Dependency injection**
- Designed for building large-scale, maintainable apps.
- Not to be confused with:
  - **AngularJS (v1.x)** – the original version (JavaScript-based)
  - **Angular 2+** – complete rewrite using TypeScript

---

## Virtual DOM

- A **programming concept** used in frameworks like **React**.
- It creates an **in-memory representation** of the real DOM.
- When a component’s state changes:
  1. A new Virtual DOM tree is created.
  2. It's compared (diffed) with the previous tree.
  3. Only the **changed parts** are updated in the real DOM.
- **Benefits:**
  - Improved performance
  - Easier to reason about UI updates

---

## React

- A **JavaScript library** for building **user interfaces**, developed by **Meta (Facebook)**.
- Focuses on **component-based architecture**.
- Uses:
  - **JSX** (JavaScript + HTML syntax)
  - **Virtual DOM**
  - **Unidirectional data flow**
- React encourages building UIs from small, reusable components.
- Can be used with various state management and routing libraries.

---

## Redux

- A **predictable state container** for JavaScript apps.
- Often used with **React**, but also works with other libraries.
- Based on three core principles:
  1. **Single source of truth** (central store)
  2. **State is read-only** (immutable updates)
  3. **Changes via pure functions** (reducers)
- Follows **Flux architecture** (developed at Facebook).
- Helps manage complex state in large applications.
- Alternatives: **Zustand**, **Recoil**, **Jotai**, **MobX**

---