NovaOS 

A single-file, browser-based desktop OS — no install, no login, just open `index.html`.

Features
- Draggable & resizable windows
- Taskbar with Start menu and open-app list
- Desktop icons (double-click to open)
- Right-click context menu
- Window edge-snapping (drag to screen edge to snap)
- Keyboard shortcuts: `Alt+T` Terminal, `Alt+N` Notepad, `Esc` close Start menu
- Live clock & date widget

Built-in Apps
- About – info about NovaOS
- Notepad – text editor with autosave (localStorage)
- Calculator – basic arithmetic
- *erminal – type `help` for commands (`theme`, `open`, `time`, `joke`, etc.)
- Devlo- development progress log
- Settings – switch between 4 themes (saved automatically)

Usage
1. Download `index.html`
2. Open it in any modern browser
3. Double-click icons or use the Start menu to launch apps

Customize
- Add new apps by adding an entry to `windowConfigs` in the `<script>` section
- Edit CSS variables/gradients to change the look
- Add new themes in `setTheme()`

No backend, no dependencies  pure HTML/CSS/JS.
