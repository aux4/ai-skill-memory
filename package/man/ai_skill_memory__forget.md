#### Description

The `forget` command removes a curated long-term memory entry by topic. It is a thin wrapper over `aux4 kb remove` against `<folder>/long-term/`. It only affects long-term memory — daily notes are never deleted by this command (they fade naturally as they age out of `recent` windows).

#### Usage

```bash
aux4 ai skill memory forget "<topic>" [--folder <folder>]
```

--topic    Topic to forget (positional, required)
--folder   Memory folder path (default: `.memory`)

#### Example

```bash
aux4 ai skill memory forget "deploy-process"
```
