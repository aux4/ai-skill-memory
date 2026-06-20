#### Description

The `recall` command searches curated **long-term memory** with `aux4 kb search` over `<folder>/long-term/` and prints the results under a **Long-term Memory** heading. The search is BM25-ranked, so the most relevant entries appear first and matches on titles and tags are surfaced — not just body text. This is the high-signal, durable tier.

`recall` intentionally does **not** search the raw daily notes. Recent daily context is already served by `recent` and `today` (which list whole days safely), and ad-hoc search across the dailies is the agent's own job using its `searchFiles`/`searchContext` tools or the `aux4 search` package. The command prints a one-line pointer to `recent`/`today` for that reason.

If there are no daily notes at all, `recall` still runs cleanly and returns long-term matches — it never touches a `daily/*.md` glob, so it cannot fail with a shell "no matches found" error.

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

(Recent daily context is available via: aux4 ai skill memory recent / today)
```
