# pinpoint — visual annotation for Claude

Click pins / drag boxes on screenshots in a browser; structured JSON flows back into the conversation.

## Install

```bash
curl -fsSL https://raw.githubusercontent.com/maferland/pinpoint-mcp/main/install.sh | bash
```

Restart Claude Code after install. Repo: `~/.pinpoint-mcp`.

## Daily flow

| Step | Command |
|---|---|
| Take screenshot (mac) | `screencapture -x /tmp/s.png` |
| Open for annotation in chat | `/pinpoint-review /tmp/s.png` |
| Multi-image review | `/pinpoint-review /tmp/before.png /tmp/after.png` |
| With context | `/pinpoint-review /tmp/s.png --context "header redesign"` |
| Bare CLI (any terminal) | `pinpoint review /tmp/s.png` |

Slash command shells out to `pinpoint review` — same flow, output goes into the conversation.

## In the browser

| Action | What it does |
|---|---|
| Click empty canvas | drop a pin |
| Drag | draw a box region |
| Click a pin | open popover, type note |
| Click empty canvas while popover open | close popover (no new pin) |
| ⌘Enter | save note |
| Esc | cancel |
| Arrow keys | switch images in filmstrip |
| Click **Done** | finalize, send back to Claude |

## Output shape

```json
{
  "context": "header redesign",
  "images": [{ "path": "/tmp/s.png", "width": 1440, "height": 900 }],
  "annotations": [
    { "number": 1, "image": "/tmp/s.png",
      "pin": { "x": 60.0, "y": 80.1 },
      "box": { "x": 60.0, "y": 80.1, "width": 12, "height": 5 },
      "comment": "Footer spacing too tight" }
  ]
}
```

Coords are **percentages** (0–100), not pixels. No intent/severity fields — Claude classifies from the comment.

## Triggering via natural language

The `using-pinpoint` skill routes to `/pinpoint-review` for phrasings like:

- "review this UI" / "what's wrong with this page"
- "let me annotate this"
- "I'll give you feedback on this"

Bare "what do you think of this image?" makes Claude *describe* it instead. To force pinpoint, say "annotate" or "use pinpoint".

## MCP back door (non-interactive)

`pinpoint-mcp` server registered alongside. Tools: `create_review`, `add_image`, `get_annotations`, `list_reviews`. Use only when scripting — slash command is the happy path.

## Dev

```bash
cd ~/.pinpoint-mcp
bun install && bun run build
bun test                  # 18 unit/integration tests
verdict run               # 5 LLM-behavior tests for the skill
bun run dev               # watch mode
```

## Pitfalls

- CLI takes a **file path**, not an inline image. Save attachments to `/tmp/` first.
- HTTP server defaults to port 4747. Override with `PINPOINT_PORT`.
- `pinpoint` must be on PATH — `bun link` from the repo root puts it in `~/.bun/bin/pinpoint`.
- Don't mix MCP `create_review` with `/pinpoint-review` in the same session — different review IDs, separate stores.

Upstream: <https://github.com/maferland/pinpoint-mcp>
