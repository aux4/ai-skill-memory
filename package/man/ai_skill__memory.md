#### Description

The `memory` skill gives an agent a two-tier memory system that survives across sessions, contributed to the shared `ai:skill` profile (`aux4 ai skill memory ...`). It is a deterministic **command skill** — the agent calls its commands directly with its own tools; there is no `run` and no LLM dependency.

The two tiers:

- **Daily notes** — the raw, append-only scratch log. One markdown file per day under `<folder>/daily/YYYY-MM-DD.md`. Cheap to write, never curated.
- **Long-term memory** — curated, topic-based, searchable, and tagged. Backed by `aux4/kb` under `<folder>/long-term/`. High-signal; distilled from daily notes during review.

Commands:

- **prompt** — print the workflow guidance (when to log vs remember, recall/review strategy). Optional deep tier.
- **log** — append a raw entry to today's daily note.
- **today** — print today's daily note.
- **recent** — print daily notes from the last N days.
- **remember** — promote a distilled insight to long-term memory.
- **recall** — search both tiers (curated long-term + raw daily notes).
- **forget** — remove a long-term memory entry.
- **review** — show recent daily notes beside current long-term memory for curation.

#### Usage

```bash
aux4 ai skill memory <command> [options]
```

#### Example

```bash
aux4 ai skill memory log "User prefers yarn over npm"
aux4 ai skill memory remember "tooling" --content "User prefers yarn, tabs" --tags prefs
aux4 ai skill memory recall "yarn"
```
