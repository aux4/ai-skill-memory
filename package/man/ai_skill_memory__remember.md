#### Description

The `remember` command promotes a distilled insight to curated long-term memory. It is a thin wrapper over `aux4 kb add`, storing one topic-based, tagged, searchable entry under `<folder>/long-term/`. Long-term memory is the tier that survives across sessions — keep entries concise and high-signal (one topic per entry); most daily notes should never be promoted.

#### Usage

```bash
aux4 ai skill memory remember "<topic>" --content "<text>" [--tags <tags>] [--folder <folder>]
```

--topic    Topic name for the memory entry (positional, required)
--content  Content to remember
--tags     Comma-separated tags (default: `memory`)
--folder   Memory folder path (default: `.memory`)

#### Example

```bash
aux4 ai skill memory remember "deploy-process" \
  --content "Always run tests before deploying" \
  --tags "deploy,process"
```
