# pi-obsidian-context

A [Pi](https://github.com/badlogic/pi-mono) extension that bridges your Obsidian vault with Pi. It surfaces the active file, open tabs, and selected text as a TUI widget and automatically injects them as hidden LLM context — so Pi knows what you're looking at in Obsidian without you having to paste it.

## Prerequisites

This extension reads a `context.json` file from your vault's `.obsidian/` directory. You need an Obsidian plugin that writes this file (for example, [obsidian-agent-context](https://github.com/xuezhaojun/obsidian-agent-context)).

The JSON file is expected to have the following shape:

```jsonc
{
  "ts": 1714500000000,
  "active": { "path": "notes/foo.md", "name": "foo.md" },
  "tabs": [
    { "path": "notes/foo.md", "name": "foo.md", "isActive": true },
    { "path": "notes/bar.md", "name": "bar.md", "isActive": false }
  ],
  "selection": {                // optional
    "text": "selected text…",
    "sourcePath": "notes/foo.md"
  }
}
```

## Install

```bash
pi install npm:pi-obsidian-context
```

## How it works

1. **Vault detection** — On session start, the extension walks up from `cwd` looking for a `.obsidian/` directory to locate your vault root.

2. **TUI widget** — A compact status line is displayed in the Pi footer showing the active file, tab count, and any current selection.

3. **LLM context injection** — Before each agent turn, the extension injects the current Obsidian state (active file, open tabs, selected text) as a hidden message so the model is aware of your editing context.

4. **Live updates** — The extension watches `context.json` for changes and refreshes the widget in real time.

## License

[MIT](LICENSE)
