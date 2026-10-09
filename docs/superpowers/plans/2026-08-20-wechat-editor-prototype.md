# Open WeChat Editor Prototype Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Deliver an immediately runnable, high-fidelity prototype of the local Markdown-to-WeChat editor described in the approved design.

**Architecture:** A dependency-free static client lives under `apps/wechat-editor`, with a small Node static server at `scripts/start-wechat-editor.mjs`. A pure Markdown renderer module produces the same HTML used by the preview, rich-text copy, and HTML export. Browser state is persisted in `localStorage`; WeChat draft controls are explicitly presented as configuration-gated prototype actions.

**Tech Stack:** HTML, CSS, browser ES modules, Node.js 18+, `node:test`.

**Visual thesis:** A calm editorial workbench: warm paper preview, graphite editing surface, restrained forest-green actions, and no dashboard-card clutter.

**Content plan:** Compact application bar; Markdown toolbar; split writing/preview workspace; sample article covering headings, quote, list, image, code, and callout; lightweight settings/dialog feedback.

**Interaction thesis:** Preview updates as the user types; save state shifts from “保存中” to “本机已保存”; toolbar and template controls give immediate visual feedback without editing the right pane.

---

### Task 1: Lock the prototype contract with tests

**Files:**
- Create: `tests/wechat-editor-prototype.test.mjs`
- Test: `tests/wechat-editor-prototype.test.mjs`

- [ ] Write tests asserting that the editor shell exposes the Markdown input, 375px preview, theme selector, local-save status, import/export/copy actions, and WeChat draft action.
- [ ] Write renderer tests asserting headings, emphasis, quote, list, code block, link, image, and unsafe HTML escaping.
- [ ] Run `node --test tests/wechat-editor-prototype.test.mjs` and confirm it fails because the prototype files do not yet exist.

### Task 2: Implement the rendering core and sample theme

**Files:**
- Create: `apps/wechat-editor/src/markdown-renderer.mjs`
- Create: `apps/wechat-editor/themes/clear-reading.json`
- Create: `apps/wechat-editor/fixtures/theme-preview.md`
- Test: `tests/wechat-editor-prototype.test.mjs`

- [ ] Implement a small deterministic renderer for the documented Markdown subset.
- [ ] Define the `clear-reading` theme tokens using the approved colors, typography, spacing, and component styles.
- [ ] Add a representative Chinese sample article.
- [ ] Run the focused test and confirm the renderer contract passes.

### Task 3: Implement the interactive editor shell

**Files:**
- Create: `apps/wechat-editor/index.html`
- Create: `apps/wechat-editor/styles.css`
- Create: `apps/wechat-editor/src/app.mjs`
- Create: `apps/wechat-editor/assets/editorial-cover.svg`
- Modify: `package.json`

- [ ] Build the split editor with a fixed-width WeChat preview and responsive fallback.
- [ ] Implement live rendering, Markdown toolbar insertion, local autosave/recovery, character counts, and preview-width controls.
- [ ] Implement `.md` import, Markdown export, HTML export, and rich-text clipboard copy using the shared rendered result.
- [ ] Add template/settings and WeChat draft dialogs that clearly distinguish configured versus unconfigured state.
- [ ] Add root `start` and `dev` commands without disturbing existing CLI commands.

### Task 4: Serve, inspect, and capture

**Files:**
- Create: `scripts/start-wechat-editor.mjs`
- Create: `output/wechat-editor-preview.png`

- [ ] Start the server with `npm start` and verify `http://127.0.0.1:3210/` returns the prototype.
- [ ] Verify editing updates the preview and persists after reload.
- [ ] Verify the 375px preview and responsive layout in a real browser.
- [ ] Capture the final page to `output/wechat-editor-preview.png`.
- [ ] Run `node --test tests/wechat-editor-prototype.test.mjs`, the complete `npm test`, and `npm run check` before reporting completion.
