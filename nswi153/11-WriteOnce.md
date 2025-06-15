# Write once, Run everywhere

A development approach where **the same codebase** can be deployed to **multiple platforms** (web, desktop, mobile, etc.).


## UI Strategy

- **Responsive** – UI layout adjusts dynamically based on screen size (e.g., grid layout, flexbox).
- **Adaptive** – UI behavior adjusts based on **input method** (e.g., keyboard, touchscreen, mouse).


## Target Platforms

- **Web** – Runs in a browser.
- **Native** – Runs directly on the operating system (compiled or via system APIs).


## Container
Runs app inside a wrapper or runtime that simulates an environment (e.g., a browser or system shell).

### Electron

- Framework for building **cross-platform desktop apps** using **web technologies** (JavaScript, HTML, CSS).
- Embeds:
  - **Chromium** (for UI rendering)
  - **Node.js** (for filesystem and OS access)
- Supports frontend frameworks like **React**, **Vue**, **Svelte**, etc.
- Pros:
  - One codebase for Windows, macOS, Linux.
  - Easy to get started.
- Cons:
  - **Heavyweight** (bundles Chromium with every app).
  - Higher memory and CPU usage.

#### Used by:
- Slack
- Discord
- Visual Studio Code
- Figma (previously)

### Cordova
- Allows building **mobile apps** with HTML, CSS, and JavaScript.
- Wraps a web application inside a native WebView.
- Uses **plugins** to access native device APIs (camera, GPS, etc.).

- Pros:
  - Easy to convert web apps to mobile apps.
- Cons:
  - Poor performance.
  - Lacks native UI look/feel.

## Bridge
Provides a translation layer between your app code and the native system (OS-level APIs, UI components).

### React Native
- Developed by **Meta (Facebook)**.
- Build **cross-platform mobile apps** using **React**, but:
  - No HTML/CSS/DOM.
  - Uses **native UI components** via a **JavaScript-to-native bridge**.
- Uses **JavaScript/TypeScript + custom stylesheets** (not CSS).

- ✅ Pros:
  - Near-native performance.
  - Large community and plugin ecosystem.
- ❌ Cons:
  - Bridge overhead can affect performance.
  - Some native features may need bridging.

#### Used by:
- Instagram
- Facebook
- Skype

## Compile to native

### Flutter
- Developed by **Google**.
- Uses **Dart** language.
- Compiles to **native ARM** or **WebAssembly** code.
- Renders using its own high-performance **Skia engine** (does not use native UI widgets).

- ✅ Pros:
  - Great performance and visual consistency across platforms.
  - One codebase for Android, iOS, Web, Desktop.
- ❌ Cons:
  - Learning curve (Dart is less common).
  - Larger app size.


## WebAssambly
- A **binary instruction format** for the web.
- Allows running **native-compiled code** (e.g., from C, C++, Rust) in the browser.
- Executes at **near-native speed**.

### Key Points:
- Does **not** have direct access to the DOM (but can communicate with JavaScript).
- Used for performance-critical web apps (e.g., image/video processing, games).
- Enables **porting desktop apps to the web**.