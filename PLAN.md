# MD Viewer — Plan

A single static HTML page that renders Markdown files client-side. Host it anywhere, bookmark it, drag-and-drop a `.md` file, and read it beautifully — nothing ever leaves your browser.

## Goals

- **Zero server-side processing** — the server only serves static assets; all rendering happens in the browser
- **No file upload** — files are read with the File API and never transmitted
- **Beautiful output** — clean typography, syntax-highlighted code blocks, proper tables, task lists, etc.
- **Single page** — one `index.html` with inlined CSS/JS (or minimal external CDN deps) so it's trivially deployable
- **Dark/light mode** — toggle + respect `prefers-color-scheme`

## Tech Stack

| Concern | Choice | Why |
|---|---|---|
| Markdown parsing | [markdown-it](https://github.com/markdown-it/markdown-it) | Fast, CommonMark-compliant, extensible via plugins |
| Syntax highlighting | [highlight.js](https://highlightjs.org/) (via `markdown-it-highlightjs` or manual integration) | Broad language support, themeable |
| Task lists | `markdown-it-task-lists` plugin | GitHub-style `- [x]` checkboxes |
| Styling | Hand-written CSS inspired by GitHub's markdown style | Keeps it small and self-contained |
| Dark mode | CSS custom properties + a toggle button | Simple, no framework needed |

All dependencies loaded from a CDN (jsDelivr) — keeps the repo to a single HTML file.

## UI / UX

### Layout

```
┌──────────────────────────────────────────────┐
│  MD Viewer                    [theme toggle]  │
├──────────────────────────────────────────────┤
│                                              │
│   ┌──────────────────────────────────────┐   │
│   │                                      │   │
│   │   Drop a .md file here               │   │
│   │   or click to browse                 │   │
│   │                                      │   │
│   └──────────────────────────────────────┘   │
│                                              │
└──────────────────────────────────────────────┘
```

After a file is loaded, the drop zone collapses into a small bar at the top showing the filename and a "change file" link, and the rendered markdown fills the page:

```
┌──────────────────────────────────────────────┐
│  README.md  [change file]    [theme toggle]  │
├──────────────────────────────────────────────┤
│                                              │
│  <rendered markdown content>                 │
│                                              │
│                                              │
└──────────────────────────────────────────────┘
```

### Interactions

1. **Drag-and-drop** a `.md` file onto the drop zone (or anywhere on the page)
2. **Click** the drop zone to open a file picker (accepts `.md`, `.markdown`, `.txt`)
3. **Paste** markdown text from clipboard (`Ctrl+V` / `Cmd+V`) when no file is loaded
4. After loading, the rendered output appears immediately
5. Dropping/picking a new file replaces the current content

## Implementation Steps

1. **Scaffold `index.html`** — basic HTML structure, CDN script/link tags for markdown-it + highlight.js
2. **Drop zone + file reader** — drag-and-drop area, click-to-browse `<input type="file">`, `FileReader` to read as text
3. **Markdown rendering** — pipe the file text through markdown-it with highlight.js integration, inject into a `<div id="content">`
4. **Styling** — CSS custom properties for colors, GitHub-flavored markdown styles (headings, code blocks, tables, blockquotes, lists, hr, images)
5. **Dark/light toggle** — button that flips a `data-theme` attribute on `<html>`, persist choice in `localStorage`
6. **Clipboard paste support** — listen for `paste` event, read text from clipboard
7. **Polish** — responsive design, smooth transitions, accessible labels, favicon

## File Structure

```
md-viewer/
├── index.html   # everything lives here
├── PLAN.md      # this file
└── README.md
```

## Non-Goals (keeping it simple)

- No editing / live preview split pane
- No table of contents sidebar
- No export to PDF/HTML
- No URL-based file loading (would need CORS headers on the source)
- No service worker / offline support (nice-to-have for later)
