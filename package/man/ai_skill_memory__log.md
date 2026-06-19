#### Description

The `log` command appends a raw entry to today's daily note — the scratch tier of the memory skill. It creates the `<folder>/daily/` directory if needed and the daily file `<folder>/daily/YYYY-MM-DD.md` if it does not exist yet (writing a `# YYYY-MM-DD` heading once), then appends the entry as a bullet point. Logging is meant to be frequent and unstructured; promote anything worth keeping to long-term memory with `remember`.

#### Usage

```bash
aux4 ai skill memory log "<entry>" [--folder <folder>]
```

--folder   Memory folder path (default: `.memory`)

#### Example

```bash
aux4 ai skill memory log "Deployed v2.3.0 to production"
```

```text
Logged to .memory/daily/2026-06-19.md
```

```bash
aux4 ai skill memory log "User prefers TypeScript" --folder /path/to/memory
```
