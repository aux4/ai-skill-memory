#### Description

The `recent` command prints the daily notes from the last N days, most recent first, separated by `---` dividers. It is the way to reload short-term context — what happened across the last few sessions — without curating anything to long-term memory.

#### Usage

```bash
aux4 ai skill memory recent [<days>] [--folder <folder>]
```

--days     Number of days to look back (default: `3`, positional)
--folder   Memory folder path (default: `.memory`)

#### Example

```bash
aux4 ai skill memory recent 5
```

```text
# 2026-06-19

- Deployed v2.3.0 to production

---

# 2026-06-18

- Investigated flaky test
```
