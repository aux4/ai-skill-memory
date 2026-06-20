# agent/skill-memory

A native aux4 agent skill that gives an agent a two-tier memory system: raw **daily notes** for in-session logging and curated **long-term memory** for what should survive across sessions. It is a deterministic **command skill** — the agent calls its commands directly with its own tools. It depends on `aux4/ai-skill` (for the shared `ai:skill` profile and the skill contract) and `aux4/kb` (long-term storage). It has no LLM dependency and no `run` command.

## Installation

```bash
aux4 aux4 pkger install agent/skill-memory
```

## Quick Start

```bash
aux4 ai skill memory log "User prefers yarn over npm"
aux4 ai skill memory remember "tooling" --content "User prefers yarn, tabs for indentation" --tags prefs
aux4 ai skill memory recall "yarn"
```

## The Two Tiers

- **Daily notes** — the raw, append-only scratch log. One markdown file per day under `<folder>/daily/YYYY-MM-DD.md`. Cheap to write, never curated. Use `log`, `today`, `recent`.
- **Long-term memory** — curated, topic-based, searchable, and tagged. Backed by `aux4/kb` under `<folder>/long-term/`. High-signal; distilled from daily notes during review. Use `remember`, `forget`.

`recall` searches the long-term tier (BM25-ranked `kb search`); recent daily context is served by `recent`/`today`. `review` shows both tiers side by side for curation. Read the full workflow guidance with `aux4 ai skill memory prompt`.

## Memory Structure

```text
.memory/
├── daily/
│   ├── 2026-06-19.md     # Today's daily note
│   ├── 2026-06-18.md     # Yesterday's daily note
│   └── ...
└── long-term/
    ├── index.md          # Table of contents (auto-maintained by kb)
    ├── deploy-process.md # Individual curated entries
    └── tooling.md
```

The memory folder defaults to `.memory` and can be overridden on any command with `--folder <path>`.

## Commands

All commands are contributed to the shared `ai:skill` profile under `memory`.

| Command | Description |
|---------|-------------|
| `aux4 ai skill memory prompt` | Print the two-tier workflow guidance (when to log vs remember, recall/review strategy) |
| `aux4 ai skill memory log "<entry>"` | Append a raw entry to today's daily note |
| `aux4 ai skill memory today` | Print today's daily note |
| `aux4 ai skill memory recent [days]` | Print daily notes from the last N days (default: 3) |
| `aux4 ai skill memory remember "<topic>" --content "<text>" [--tags <tags>]` | Promote a distilled insight to long-term memory |
| `aux4 ai skill memory recall "<query>"` | Search curated long-term memory (BM25-ranked); use `recent`/`today` for daily context |
| `aux4 ai skill memory forget "<topic>"` | Remove a long-term memory entry |
| `aux4 ai skill memory review [days]` | Show recent daily notes beside current long-term memory for curation |

## Native Skill Contract

This package conforms to the native aux4 skill contract:

- **scope `agent`, name `skill-memory`** — depends on `aux4/ai-skill` only (plus `aux4/kb` for storage); never on `aux4/ai-agent` or `aux4/copilot`.
- **`help.text` everywhere** — the required discovery layer (`aux4 ai skill memory --help`).
- **`man/ai_skill_memory__<command>.md`** — the per-command "is this a good fit?" tier.
- **`prompt`** — the optional deep guidance tier, provided because memory is a non-trivial two-tier workflow.
- **No `run`** — running a skill is a runtime concern of `aux4/ai-agent`, not the skill itself.

Verify conformance:

```bash
aux4 ai skill validate memory
aux4 ai skill list
```

## License

This package is licensed under the Apache-2.0 License.

See [LICENSE](./LICENSE) for details.
