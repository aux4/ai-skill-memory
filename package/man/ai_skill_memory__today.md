#### Description

The `today` command prints today's daily note (`<folder>/daily/YYYY-MM-DD.md`). If no note has been written today, it prints a short notice instead of erroring. Use it to recall what has already been logged in the current session.

#### Usage

```bash
aux4 ai skill memory today [--folder <folder>]
```

--folder   Memory folder path (default: `.memory`)

#### Example

```bash
aux4 ai skill memory today
```

```text
# 2026-06-19

- Deployed v2.3.0 to production
```
