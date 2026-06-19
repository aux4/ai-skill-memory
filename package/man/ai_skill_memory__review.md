#### Description

The `review` command supports the curation workflow: it prints the recent daily notes (last N days, most recent first) under **Daily Notes for Review**, followed by the current long-term memory index (`aux4 kb list`) under **Current Long-term Memory**. Read through the recent days, promote what matters with `remember`, update existing long-term entries when new information changes them, and let the rest fade. Most daily entries are ephemeral by design.

#### Usage

```bash
aux4 ai skill memory review [<days>] [--folder <folder>]
```

--days     Number of days to review (default: `7`, positional)
--folder   Memory folder path (default: `.memory`)

#### Example

```bash
aux4 ai skill memory review 7
```

```text
## Daily Notes for Review

# 2026-06-19

- Deployed v2.3.0 to production

---

## Current Long-term Memory

| Topic | File | Tags | Date | Summary |
|-------|------|------|------|---------|
| deploy-process | deploy-process.md | deploy,process | 2026-06-19 | Always run tests... |
```
