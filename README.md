# MD Viewer

A single static HTML page that renders Markdown files client-side. Host it anywhere, bookmark it, drag-and-drop a `.md` file, and read it beautifully -- nothing ever leaves your browser.

## Features

- **Drag-and-drop** or click to browse for `.md`, `.markdown`, `.txt` files
- **Paste** markdown from clipboard (Ctrl+V / Cmd+V)
- **Syntax highlighting** via highlight.js
- **YAML frontmatter** support -- parsed and displayed as a styled metadata card (title, tags as badges, key-value pairs, lists)
- **GitHub-style** rendering with tables, task lists, blockquotes, and more
- **Dark/light mode** toggle with system preference detection and localStorage persistence
- **Zero server-side processing** -- everything runs in the browser
- **Single file** -- just `index.html`, no build step

## Usage

**Go to [micheleb.github.io/md-viewer](https://micheleb.github.io/md-viewer/)** and drop a file in.

Or clone / download the repo and open `index.html` directly in your browser -- no server needed.

## Tech Stack

- [js-yaml](https://github.com/nodeca/js-yaml) for YAML frontmatter parsing
- [markdown-it](https://github.com/markdown-it/markdown-it) for Markdown parsing
- [highlight.js](https://highlightjs.org/) for syntax highlighting
- [markdown-it-task-lists](https://github.com/revin/markdown-it-task-lists) for GitHub-style checkboxes
- All dependencies loaded from CDN (jsDelivr)
