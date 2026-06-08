# Selector

Point at any element. Tell your AI what to change.

A bookmarklet that lets you visually select elements on any web page, add instructions, and copy a structured prompt — paste it into Claude Code, Codex, Cursor, or any AI coding assistant.

[中文文档](README.zh-CN.md)

## Install

1. Visit the **[install page](https://oil-oil.github.io/selector/)**
2. Drag the **Selector** button to your bookmarks bar (one-time)
3. Done

## Usage

Open any web page, click the **Selector** bookmark.

| Action | What it does |
|---|---|
| **Click** | Select an element |
| **Shift + Click** | Add to selection |
| **Drag** | Marquee select multiple elements |
| **↑ / ↓** | Navigate to parent / child element |
| **← / →** | Navigate to previous / next sibling |
| **✎ button** | Add per-element instruction |
| **⌘C** | Copy prompt to clipboard |
| **⌘Z** | Undo last selection change |
| **Space** | Pause / resume selecting |
| **Esc** | Clear selection |

## Features

### Element Selection
- Click to select any visible element on the page
- Shift+click to multi-select
- Drag to marquee-select multiple elements
- Arrow keys to navigate DOM hierarchy
- Per-element instructions via annotate button

### Context-Aware Metadata
- CSS selectors with full path
- React component names (development mode)
- Source file references (React dev mode)
- Text content and HTML snippets
- Data attributes

### Advanced Support (v2.0)
- **iframe Support** - Select elements inside same-origin iframes (marked with 📄)
- **Shadow DOM Support** - Select elements inside Shadow DOM (marked with 🔲)
- **Dynamic Detection** - Automatically detects and binds to dynamically added iframes
- **Self-Healing** - Auto-repairs event listeners when iframe content changes

## Example output

```
Page: /dashboard

1. .hero-title <h1>
   selector: body > main > section > h1
   source: src/components/Hero.tsx:12
   react: Layout › Hero
   text: "Welcome to the Dashboard"
   html: <h1 class="hero-title">Welcome to the Dashboard</h1>
   instruction: Make this red and larger

2. .sidebar-btn <button> 📄 https://example.com/preview
   selector: iframe[preview] > button.sidebar-btn
   text: "Click Me"
   html: <button class="sidebar-btn">Click Me</button>

3. .custom-element <div> 🔲 shadow:my-component
   selector: shadow:my-component > .custom-element
   text: "Shadow DOM content"
```

## How it works

The bookmarklet injects `editor.css` + `editor.js` into the current page. Everything runs client-side — no data is sent anywhere. The code is bundled into the bookmark at install time, so it works offline after that.

### iframe Support
The tool automatically detects same-origin iframes and injects event listeners into their documents. Elements inside iframes are visually distinguished with a purple border and marked with 📄 in the output.

### Shadow DOM Support
Elements inside Shadow DOM roots are also selectable. They're shown with a green border and marked with 🔲 in the output.

### Cross-Origin Limitations
Due to browser security policies, elements inside cross-origin iframes cannot be selected. These iframes are automatically detected and skipped.

## Development

```bash
git clone https://github.com/oil-oil/selector.git
cd selector
# Edit assets/editor.js and assets/editor.css
# Test locally: python -m http.server 8080
# Then visit http://localhost:8080
# Push to main — GitHub Pages auto-deploys
```

## License

MIT
