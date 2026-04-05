# PQ-Stego Frontend Design Document

## 1. Overview
The **PQ-Stego** frontend is a lightweight Single Page Application (SPA) designed to serve as the user interface for a post-quantum steganography system. It provides a highly specialized, immersive, and interactive experience tailored for cybersecurity. 

The application strictly utilizes **Vanilla HTML, CSS, and JavaScript** without relying on component-based frameworks (like React, Vue, or Angular) or utility-first CSS libraries (like Tailwind CSS). This ensures a minimal footprint, complete control over the DOM, and avoids build steps (such as Webpack or Vite), directly serving static assets via an Nginx/Python server.

---

## 2. Architecture & Design Patterns

### 2.1 Single Page Application (SPA) Routing Pattern
The application handles navigation internally without triggering full page reloads:
- **View Containers**: All "pages" (Landing, Embed Form, Embed Result, Extract Keys, Extract Files, Extract Result) are represented by distinct `<section>` elements with a `.view` class.
- **State Switcher**: The `navigateTo(viewId)` JavaScript function manages navigation by iterating over all `.view` sections, hiding them (removing the `.active` class), and showing only the target view. This operates as a rudimentary but effective in-memory client-side router.

### 2.2 DOM-driven State Management
No external state container (like Redux) is used. 
- Transitory application state (e.g., entered keys, orchestrator API responses) is kept in global variables (`embedResponse`, `extractKeys`) within `app.js`.
- Security is prioritized: sensitive objects like PQC extraction keys are explicitly **held in memory only** and are wiped upon page refresh.

### 2.3 Component Rendering Pattern
UI structures like file lists, statistic grids, cryptographic key readouts, and download cards are rendered recursively using vanilla JavaScript Template Literals (`innerHTML`) dynamically injecting API data securely into the DOM.

---

## 3. Design Aesthetics & Theming

The application explicitly employs a **Cybersecurity Dark Theme**, designed to evoke a modern, secure, terminal-like ambiance. It utilizes glowing elements, high-contrast typography, and atmospheric background animations.

### 3.1 Color Palette
CSS custom properties (design tokens) are strictly maintained in the `:root` scope to keep the theme consistent. 

**Backgrounds**
- `Primary Background`: `#050505` (Almost pitch black)
- `Secondary Background`: `#0a0f0a` (Deep dark green-tinted black)
- `Card Background`: `rgba(10, 25, 15, 0.85)` (Translucent container color)
- `Input Surface`: `#0d1a10` (Dark background for forms with deep green tint)

**Accent Colors (The "Matrix" Green Scheme)**
- `Neon Green (Primary Accent)`: `#00ff88` (Used for highlights, strong glows, active states)
- `Mid Green`: `#00cc6a` (Used for secondary accents, icons, hover states)
- `Dark Green`: `#003c1f` (Used for gradients, borders, spinner base)

**Text & Typography Colors**
- `White`: `#e8ece8` (Main body text)
- `Dim White`: `#a0a8a0` (Labels, subtitles)
- `Muted White`: `#5a665a` (Helper text, deactivated text)

**Status Colors**
- `Error / Alert Red`: `#ff4444` (Combined with a translucent red background `rgba(255, 68, 68, 0.15)`)
- `Warning Yellow`: `#ffd700`

**Glows and Shadows**
- The UI relies heavily on `<box-shadow>` effects casting `rgba(0, 255, 136, 0.15)` (Green Glow) and `rgba(0, 0, 0, 0.4)` (Card Depth) to give elements neon-luminescence and physical elevation over the terminal matrix backdrop.

### 3.2 Typography
The application uses Google Fonts directly to define two distinct font families:
- **Body & Headlines**: `Inter` (sans-serif) — Used for modern, clean readability of labels, paragraphs, and standard UI components.
- **Data & Cryprography**: `JetBrains Mono` (monospace) — Exclusively used for application titles, keys, hexadecimal strings, statistical values, and logs.

---

## 4. UI Structure & Components

### 4.1 Base Layout
The interface utilizes a max-width container (`max-width: 900px`) centered on the screen, overlaying a background canvas.

### 4.2 Interactive Components
- **Drag-and-Drop Zones (`.dropzone`)**: Reusable UI blocks with dashed borders (`2px dashed var(--border)`). They use JS DataTransfer objects internally to maintain file arrays. Visually they pulse with a green glow (`rgba(0, 255, 136, 0.15)`) upon hover indicating interactability.
- **Glassmorphism Cards (`.card`)**: Contains sections of forms and results. Includes `backdrop-filter: blur(10px)` to softly blur the matrix background behind transparent overlays. 
- **Solid and Ghost Buttons (`.btn-primary`, `.btn-secondary`)**: Primary buttons use a linear gradient ranging from dark green to deep green (`linear-gradient(135deg, var(--green-dark), #004d28)`) paired with inset box-shadow glows. Secondary buttons are transparent with thin borders.
- **Forms (`.form-input`, `.form-textarea`)**: Form fields maintain the dark palette, highlighting their borders with the neon green token (`--border-focus`) when active to provide accessibility feedback.
- **Alert Banners (`.error-alert`, `.success-banner`)**: Conditionally displayed elements leveraging CSS keyframe animations (shake effect) to draw user attention for errors.

### 4.3 Visual Effects
- **Matrix Rain Background (`.matrix-bg`)**: A continuous visual animation handled purely in Vanilla JS generating falling Japanese script/numbers in `.matrix-column` elements dropping vertically using CSS `@keyframes matrix-fall`. Opacity is kept at a very subtle `0.04` to maintain readability without overwhelming the interface.
- **Loading Overlay (`.loading-overlay`)**: A `z-index: 1000` blurred overlay taking over the screen during async process, featuring a dual-colored spinning ring icon rendering feedback to the user on pending cryptographic actions.

---

## 5. Frontend Logic & Libraries

### 5.1 Native Web APIs utilized
- **`fetch()` API**: Used exclusively for communicating with the backend Python orchestrator (REST layout). Handling standard HTTP mechanisms and async `Promises` natively.
- **`FormData` Interface**: Crucially used for building multipart/form-data payloads encoding raw binary data of the `.pgm` and `.wav` media files combined with plain text strings.
- **`DataTransfer` interface**: Utilized tightly with the Drag and Drop API events (`dragover`, `drop`) to append files visually maintaining synchronized file queues outside of normal `<input type="file">` constraints.
- **`Blob` & `URL.createObjectURL`**: Used to construct secure, cross-origin safe endpoints allowing the client logic to download steganographic output files identically as generated on the backend memory to preserve intricate embedded bit mappings against browser interference.
- **Clipboard API**: Integrated securely using `navigator.clipboard.writeText()` for effortless extraction of post-quantum keys and successfully decrypted plaintext.

### 5.2 Performance / Complexity Constraints
The app handles potentially large image and audio files within the browser context efficiently by only extracting standard metadata to display (sizes, file names). Large files are bypassed directly into `FormData` rather than read by the browser using slow `FileReader` memory caches.

## 6. Summary
The PQ-Stego UI accurately manifests the functional purpose of post-quantum AI steganography. By rejecting heavy frameworks in favor of modular vanilla JS, and avoiding utility classes in favor of robust CSS variables and custom properties, the frontend operates exceedingly fast, requires no build-step, and achieves a flawless, highly custom cybersecurity-oriented user experience.
