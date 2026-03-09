# MD Viewer

A single static HTML page that renders Markdown files client-side. Host it anywhere, bookmark it, drag-and-drop a `.md` file, and read it beautifully -- nothing ever leaves your browser.

## Features

- **Drag-and-drop** or click to browse for `.md`, `.markdown`, `.txt` files
- **Paste** markdown from clipboard (Ctrl+V / Cmd+V)
- **Syntax highlighting** via highlight.js
- **GitHub-style** rendering with tables, task lists, blockquotes, and more
- **Dark/light mode** toggle with system preference detection and localStorage persistence
- **Zero server-side processing** -- everything runs in the browser
- **Single file** -- just `index.html`, no build step

## Usage

Open `index.html` in a browser. That's it.

Or serve it from any static host:

```bash
npx serve .
# or
python3 -m http.server
```

## Tech Stack

- [markdown-it](https://github.com/markdown-it/markdown-it) for Markdown parsing
- [highlight.js](https://highlightjs.org/) for syntax highlighting
- [markdown-it-task-lists](https://github.com/revin/markdown-it-task-lists) for GitHub-style checkboxes
- All dependencies loaded from CDN (jsDelivr)
