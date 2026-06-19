#### Description

The `prompt` command prints the memory skill's workflow guidance — the deeper "when and how" tier of the native skill contract. It explains the two-tier model (raw daily notes vs curated long-term memory), when to `log` versus when to `remember`, how to `recall` across both tiers, and how to `review` and curate. An agent loads this on demand only when it actually engages the memory skill; for simple log/recall calls the per-command `--help` is enough.

This command reads `instructions/memory.md` from the package directory and writes it to stdout. It is optional under the native skill contract but provided here because memory is a non-trivial two-tier workflow.

#### Usage

```bash
aux4 ai skill memory prompt
```

#### Example

```bash
aux4 ai skill memory prompt
```

```text
# Memory Skill

You have two kinds of memory. Use both.
...
```
