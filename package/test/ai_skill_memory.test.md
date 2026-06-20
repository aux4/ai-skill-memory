# ai skill memory

Deterministic command-skill tests for the migrated `agent/skill-memory` package.
These assume the package is installed locally so the shared `ai:skill` profile and the
`aux4 ai skill validate`/`list` framework commands can discover it:

```bash
aux4 aux4 releaser install --dir packages/ai/skill-memory/package --noBuild true
```

## beforeAll

```execute
rm -rf /tmp/aux4-skill-memory-test && mkdir -p /tmp/aux4-skill-memory-test/daily /tmp/aux4-skill-memory-test/long-term
```

## afterAll

```execute
rm -rf /tmp/aux4-skill-memory-test
```

## prompt

### should output memory workflow guidance

```execute
aux4 ai skill memory prompt
```

```expect:partial
# Memory Skill
```

### should reference the native ai skill memory command path

```execute
aux4 ai skill memory prompt
```

```expect:partial
aux4 ai skill memory log
```

### should NOT reference the old copilot skills path

```execute
aux4 ai skill memory prompt | grep -c "copilot skills memory" || true
```

```expect
0
```

### should include the rules section

```execute
aux4 ai skill memory prompt
```

```expect:partial
## Rules
```

## command help

### log should show entry parameter

```execute
aux4 ai skill memory log --help
```

```expect:partial
The text to log
```

### remember should show content parameter

```execute
aux4 ai skill memory remember --help
```

```expect:partial
Content to remember
```

### recall should show query parameter

```execute
aux4 ai skill memory recall --help
```

```expect:partial
Search query
```

### forget should show topic parameter

```execute
aux4 ai skill memory forget --help
```

```expect:partial
Topic to forget
```

## daily log round-trip

### should log an entry

```execute
aux4 ai skill memory log "test entry from skill-memory" --folder /tmp/aux4-skill-memory-test
```

```expect:partial
Logged to
```

### today should read it back

```execute
aux4 ai skill memory today --folder /tmp/aux4-skill-memory-test
```

```expect:partial
test entry from skill-memory
```

### recent should include it

```execute
aux4 ai skill memory recent 3 --folder /tmp/aux4-skill-memory-test
```

```expect:partial
test entry from skill-memory
```

## long-term round-trip

### remember should save to long-term memory

```execute
aux4 ai skill memory remember "test-topic" --content "This is a curated test memory" --tags "test" --folder /tmp/aux4-skill-memory-test
```

```expect:partial
test-topic
```

### recall should find the long-term entry

```execute
aux4 ai skill memory recall "curated" --folder /tmp/aux4-skill-memory-test
```

```expect:partial
## Long-term Memory
```

### forget should remove the long-term entry

```execute
aux4 ai skill memory forget "test-topic" --folder /tmp/aux4-skill-memory-test
```

```expect:partial
test-topic
```

### recall after forget should report no long-term match

```execute
aux4 ai skill memory recall "curated" --folder /tmp/aux4-skill-memory-test
```

```expect:partial
No matches found.
```

## recall with no daily notes (zsh glob bug)

This is the AGC-010 regression scenario: a memory folder that has long-term
entries but **no `daily/` directory at all**. The old `recall` ran a bare
`grep -rl ${folder}/daily/*.md`, which under zsh aborts the whole command with
`zsh:1: no matches found`. The fixed `recall` searches long-term only and must
return matches with no shell error.

```beforeAll
rm -rf /tmp/aux4-skill-memory-nodaily && mkdir -p /tmp/aux4-skill-memory-nodaily/long-term
aux4 ai skill memory remember "no-daily-topic" --content "Recall must work without any daily notes present" --tags "test" --folder /tmp/aux4-skill-memory-nodaily
```

```afterAll
rm -rf /tmp/aux4-skill-memory-nodaily
```

### recall should find the long-term entry with no dailies present

```execute
aux4 ai skill memory recall "daily" --folder /tmp/aux4-skill-memory-nodaily
```

```expect:partial
## Long-term Memory
```

### recall should surface the matching entry content (BM25)

```execute
aux4 ai skill memory recall "daily" --folder /tmp/aux4-skill-memory-nodaily
```

```expect:partial
no-daily-topic
```

### recall must NOT print a zsh no-matches glob error

```execute
aux4 ai skill memory recall "daily" --folder /tmp/aux4-skill-memory-nodaily 2>&1 | grep -c "no matches found" || true
```

```expect
0
```

### recall must NOT glob the daily directory at all

```execute
grep -c "daily/\*.md" ../.aux4 || true
```

```expect
0
```

## review

### should show daily notes and long-term sections

```execute
aux4 ai skill memory review 7 --folder /tmp/aux4-skill-memory-test
```

```expect:partial
## Daily Notes for Review
```

## native skill contract

### should be registered under the ai:skill profile

```execute
aux4 ai skill memory --help
```

```expect:partial
Two-tier memory
```

### validate should pass

```execute
aux4 ai skill validate memory
```

```expect:partial
conforms to the native skill contract
```

### list should show memory

```execute
aux4 ai skill list
```

```expect:partial
memory
```

### should NOT expose a run command

```execute
aux4 ai skill memory --help | grep -c "  run" || true
```

```expect
0
```

### should NOT delegate to ai agent ask

```execute
grep -c "ai agent ask" ../.aux4 || true
```

```expect
0
```
