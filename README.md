NovaOS — Digital Garden

A fully self-contained, single-file browser-based desktop OS simulation with an AI assistant, file system, notes, calendar, automations, and more — all styled as a soft botanical "digital garden."

 Overview

NovaOS (file: `NOVA_OS__1_.html`) is a single HTML file that renders an entire operating-system-like environment inside any modern web browser. No server, no build step, no dependencies to install — just open the file. All state is persisted in `localStorage`.

The aesthetic is inspired by nature: muted greens, creams, and teals, with organic morphing shapes, glassmorphism panels, and three carefully chosen typefaces (Fraunces, Sora, JetBrains Mono).

Quick Start

```bash
# No installation needed
open NOVA_OS__1_.html     # macOS
start NOVA_OS__1_.html    # Windows
xdg-open NOVA_OS__1_.html # Linux
```

On first launch an animated boot sequence plays, followed by an onboarding checklist. A guided **Demo Tour** (7 steps) is available from the HUD bar.

Architecture

The entire application is a single HTML file split into three logical sections:

| Section | Description |
|---|---|
| `<style>` (~600 lines) | CSS custom properties (design tokens), component styles, animations |
| `<body>` (HTML) | Static scaffolding — boot screen, desktop, dock, overlays |
| `<script>` (~4500 lines) | All application logic in plain vanilla JS |

There are **no external runtime dependencies**. Google Fonts are loaded via CDN link tag; everything else is self-contained.

 Design Tokens (CSS Variables)

```css
--bg-0: #F4F5EF        /* primary background */
--accent: #35858E      /* teal accent */
--accent-2: #7DA78C    /* sage green */
--accent-3: #F58F5C    /* warm orange */
--moss: #C2D099
--font-display: 'Fraunces'
--font-body: 'Sora'
--font-mono: 'JetBrains Mono'
--radius: 18px
```


Features

Desktop Shell
- Boot screen — animated morphing blob logo + progress bar + console log lines
- HUD top bar — clock, XP bar, notification bell, sound toggle, focus mode, command palette trigger
- Workspace switcher — 3 named workspaces (School / Coding / Creative), each maintaining independent open windows
- Orbital Dock — semicircular app launcher at the bottom, with dashed orbit rings and hover labels
- Core Launcher — pulsing morphing blob at dock center; click for a predictive app launcher (shows apps ranked by recent usage probability)
- Desktop right-click menu — New Note, New Folder, Ask Nexus, Memory Constellation, Moodboard, Search, Change Wallpaper
- Widget rail — left-side panel with clock widget, activity pulse bars, and an inspirational quote

Window Manager (`WM`)
- Draggable, resizable windows with snap-to-edge preview
- Titlebar controls: minimize, maximize/restore, close
- Z-index stacking (last-clicked window becomes active)
- Window open/close animations

 Apps

| App ID | Icon | Description |
|---|---|---|
| `home` | 🏠 | Dashboard — session stats, recent activity, AI suggestions |
| `notes` | 📝 | Rich-text note editor with tags, favorites, recycle bin, checklist support, undo history |
| `explorer` | 📁 | Virtual file system — folders, files, drag-and-drop move, rename, delete, tag, favorites |
| `code` | 💻 | Syntax-aware text editor for `.js`/`.ts`/`.json` files |
| `calendar` | 📅 | Monthly calendar with click-to-add events, star/favorite events |
| `assistant` | ✨ | "Nexus" AI assistant — natural language commands to create notes/files/folders, open apps, set reminders, query activity log; powered by the Anthropic API (`claude-sonnet-4-6`) |
| `constellation` | 🌌 | Memory Constellation — canvas-based star map of all notes and files, color-coded by type, click to open |
| `timeline` | 📜 | Chronological activity log, filterable by kind (note / file / calendar / AI / system) |
| `automations` | ⚡ | Rule engine — trigger + action pairs (e.g. "when file created → show notification") |
| `habits` | 🌿 | Habit tracker — daily check-ins, streak counter |
| `pomodoro` | 🍅 | Pomodoro timer (25 / 5 min work-break cycles) |
| `moodboard` | 🎨 | Freeform canvas with sticky notes, shapes, and text elements |
| `widget-creator` | 🧩 | Create custom desktop widgets with a live HTML/CSS editor |
| `legacy-tree` | 🌳 | Visual "legacy tree" — personal milestones rendered as branching nodes |
| `settings` | ⚙️ | Theme switcher (4 themes), wallpaper selector (gradient presets + custom URL), font scale |
| `recycle-bin` | 🗑️ | Recover or permanently delete trashed notes and files |

AI Assistant (Nexus)
- Calls **Anthropic Messages API** (`/v1/messages`, model `claude-sonnet-4-6`)
- Parses natural language to dispatch system commands: create note, create file/folder, open app, set reminder, search activity
- Voice input via browser Web Speech API (microphone button)
- Conversation history maintained per session
- Interaction count tracked for XP and session summary

Gamification / XP System
- XP awarded for creating notes (+4), files (+3), folders (+2), AI interactions (+1), automations (+5), habits (+6)
- XP bar in HUD top
- Achievement toasts for milestones
- Day streak counter
- Session summary card (shown on demand) — time active, counts per category, "session mood" message

Productivity Modes
- **Focus Mode** — dims UI chrome, hides dock/widgets, adds vignette overlay; toggled from HUD
- **Dream Mode** — full-screen animated canvas particle field; click anywhere to exit

Command Palette
- Trigger: `Cmd/Ctrl + K` or HUD button
- Fuzzy search across all apps and actions
- Keyboard navigable (↑ ↓ Enter Escape)

Notifications
- Slide-in notification panel (right edge)
- Toast system — auto-dismissing with progress bar, optional action buttons
- Automation-triggered notifications

Persistence
All state (notes, files, calendar events, habits, settings, XP, activity log, favorites, tags) is serialized to `localStorage` under the key `nexusOS_state`.

Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Cmd/Ctrl + K` | Open command palette |
| `Escape` | Close command palette / exit Focus Mode |

heming

Four built-in themes (configured in Settings):

| Theme | Character |
|---|---|
| `garden` (default) | Soft greens and cream |
| `night` | Dark slate with teal accents |
| `rose` | Warm pinks and blush |
| `ocean` | Deep blues and aqua |

Themes remap the CSS custom property palette at runtime via JavaScript.

File Structure (virtual FS)

The in-memory file system (`FS` object) mirrors a real directory tree:

```
/ (root)
├── <folders you create>
│   └── <files you create>
└── <files you create>
```

Files have: `name`, `ext`, `content`, `created`, `tags[]`
Folders have: `name`, `children[]`, `created`, `tags[]`

---

Browser Compatibility

Requires a modern browser with support for:
- CSS `backdrop-filter`, `mask-image`, CSS custom properties
- `localStorage`
- `Canvas 2D API`
- `contentEditable` + `execCommand` (rich text editor)
- Web Speech API (optional, for voice input in assistant)
- Fetch API (for Anthropic API calls in assistant)

Tested on Chrome 120+, Firefox 121+, Safari 17+.

 Known Limitations

- No real persistence beyond `localStorage`** — clearing browser data erases all notes and files.
- No multi-user support — single user, single browser.
- AI assistant requires a live Anthropic API connection** — works only when the file is served in an environment where the API key is injected (e.g., Claude.ai Artifacts context).
- `execCommand` (used by the rich-text note editor) is deprecated in some browsers but still broadly supported.
- Mobile layout is functional but not fully optimized — designed primarily for desktop viewports.
