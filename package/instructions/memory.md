# Memory Skill

You have two kinds of memory. Use both.

**Daily notes** are your raw log -- what happened today, what was decided, what you learned. Append freely. Don't overthink structure. These are scratch notes, not documentation.

**Long-term memory** is curated wisdom -- user preferences, recurring patterns, important decisions, key outcomes. This is what survives. It's distilled from daily notes during reviews.

## Commands

| Command | Description |
|---------|-------------|
| `aux4 ai skill memory log "<entry>"` | Append to today's daily note |
| `aux4 ai skill memory today` | Read today's daily note |
| `aux4 ai skill memory recent [days]` | Read daily notes from the last N days (default: 3) |
| `aux4 ai skill memory remember "<topic>" --content "<text>" [--tags <tags>]` | Save to long-term memory |
| `aux4 ai skill memory recall "<query>"` | Search across both daily notes and long-term memory |
| `aux4 ai skill memory forget "<topic>"` | Remove a long-term memory entry |
| `aux4 ai skill memory review [days]` | List recent daily notes and long-term memory for curation |

## How Memory Works

**Daily notes** live in `.memory/daily/YYYY-MM-DD.md`. One file per day. Entries are appended as bullet points. These accumulate naturally -- you don't need to organize them. They're a journal, not an encyclopedia.

**Long-term memory** lives in the `.memory/long-term/` knowledge base. Entries are topic-based, searchable, and tagged. This is the curated layer -- only promote things here that are worth remembering across sessions.

## When to Log

Log things that might matter later:
- Key decisions and why they were made
- User preferences you discover ("prefers tabs over spaces", "uses yarn not npm")
- Outcomes of significant tasks
- Problems encountered and how they were solved
- Important context the user shared

Don't log routine operations or things that are obvious from the codebase.

## When to Remember (Long-term)

Promote to long-term memory when:
- A pattern repeats across multiple sessions
- The user explicitly asks you to remember something
- A decision has lasting implications
- You discover a strong user preference

Don't promote every daily note. Most daily entries are ephemeral -- that's fine. Long-term memory should be lean and high-signal.

## Reviewing and Curating

The `review` command shows recent daily notes alongside current long-term memory. Use it to:

1. **Read through recent days** -- look for patterns, recurring themes, important outcomes
2. **Promote** what matters -- use `remember` to save distilled insights to long-term memory
3. **Update** existing long-term entries if new information changes them
4. **Let the rest go** -- daily notes fade naturally. Not everything needs to be preserved.

Think of it like a human reviewing their journal: most entries are context that served their purpose. A few contain insights worth keeping.

## Recall Strategy

When searching memory with `recall`:
- Results come from both tiers -- long-term memory (structured) and daily notes (grep matches)
- Long-term results are more reliable -- they've been curated
- Daily results give raw context -- useful for recent events
- If you need more detail from a daily match, read that day's full note with `today` or `recent`

## Rules

- Log naturally during sessions -- don't wait until the end to dump everything
- When the user says "remember this", save it to long-term immediately with `remember`
- Keep long-term entries concise and specific -- one topic per entry
- Use meaningful tags on long-term entries for better search
- Don't fabricate memories -- only record what actually happened
- Review periodically -- daily notes without review just accumulate noise
