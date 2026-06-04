# claude-session-tools

Browse and read your [Claude Code](https://claude.com/claude-code) session history in the browser. Two small, dependency-free Python scripts that read the `.jsonl` transcripts Claude Code writes under `~/.claude/projects/`.

- **`session-explorer`** — a local web app indexing *every* session, grouped by project, newest-first, with live search. Click any session to read it.
- **`session-view`** — renders a single session `.jsonl` to a self-contained HTML page (user/assistant turns, thinking, tool calls + results, collapsible).

## Requirements

- Python ≥ 3.8 (standard library only — no `pip install`)
- A web browser

## Install

```sh
git clone https://github.com/<you>/claude-session-tools.git
cd claude-session-tools
chmod +x session-view session-explorer
# put them on your PATH, e.g.:
ln -s "$PWD/session-view" "$PWD/session-explorer" ~/.local/bin/
```

Keep the two scripts together — `session-explorer` loads `session-view` from the same folder (or `~/bin`).

## Usage

```sh
session-explorer                 # opens the index of all sessions in your browser
session-explorer --port 8080     # pin a port
session-explorer --no-open       # just serve; don't launch a browser

session-view path/to/session.jsonl          # renders + opens one session
session-view session.jsonl -o out.html --no-open
```

Sessions are read from `~/.claude/projects/`. Override with `CLAUDE_PROJECTS=/path session-explorer`.

## Notes

- Read-only — never modifies your transcripts. The server binds to `127.0.0.1` only.
- Titles use a session's custom name → AI title → first prompt; explicitly-named sessions are **bold**.
- Each session is rendered **linearly**. A single session file can contain branches (e.g. resuming the same session in two terminals so it diverges) — those are currently flattened into one transcript rather than shown as a tree.

## License

MIT — see [LICENSE](LICENSE).
