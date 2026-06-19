#### Description

The `recall` command searches both memory tiers and prints the results under two headings. **Long-term Memory** results come from `aux4 kb search` over `<folder>/long-term/` — these are curated and reliable. **Daily Notes** results come from grepping the daily files in `<folder>/daily/` (up to the 5 most recent matching days) — these are raw and give recent context. When a daily match needs more detail, read that day's full note with `today` or `recent`.

#### Usage

```bash
aux4 ai skill memory recall "<query>" [--folder <folder>]
```

--query    Search query (positional, required)
--folder   Memory folder path (default: `.memory`)

#### Example

```bash
aux4 ai skill memory recall "deploy"
```

```text
## Long-term Memory
deploy-process: Always run tests before deploying

## Daily Notes
### 2026-06-19
- Deployed v2.3.0 to production
```
