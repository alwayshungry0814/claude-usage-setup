# Claude Usage Setup Prompt

One prompt that sets up your global `CLAUDE.md` so Claude Code gets you the best results for the least usage: when to orchestrate, which subagents to run, how much effort to spend, and how to keep context small.

From the video **"Double Your Claude Usage Limit"**. In my tests, Opus alone matched Opus + Haiku subagents on a simple build while using a fraction of the tokens. Subagents only paid off on big, parallel search work. The rule: the task has to justify the orchestrator.

## How to use it

1. Open Claude Code.
2. Paste the prompt below.
3. Review the section Claude proposes, then let it save.

## The prompt

```
Set up my global CLAUDE.md (~/.claude/CLAUDE.md) so you get me the best results for the least usage.

1. Review how I use you: have a Haiku subagent skim my recent sessions in ~/.claude/projects/ (my prompts only) and return a 5-bullet summary of my common task types.
2. Then add a short "Usage" section (under 25 lines), tuned to that summary, covering:
   - Default: do the work yourself in the main session. No subagents for small or tightly coupled tasks.
   - Delegate only when the task justifies it: 3+ independent pieces, or more than ~10 files or sources to read, and each piece can come back as a short summary. Each subagent costs ~35–75k tokens to start, so never spawn one for less work than that.
   - Pick the cheapest capable model per subagent: Haiku for search, reading, summaries and running tests; Sonnet for real coding; Opus only if the others would fail (tell me when).
   - Keep "one best answer" work in the main session.
   - Keep context small: read targeted sections, not whole large files; don't paste long logs; prefer text over screenshots. Tell me when a fresh session or /compact would help.
   - Effort: run subagents at low or medium effort unless the piece is hard. Tell me when this session's task needs a higher effort level, or would be fine on Sonnet or at lower effort.
   - Quality first: never trade correctness for savings. Give every subagent a standalone brief with acceptance criteria, verify its results, and redo shaky work on a stronger model.
3. Show me the section before saving. Keep whatever is already in my CLAUDE.md, and merge rather than duplicate.
```

## Why these rules

- **Context is the biggest cost.** Every turn re-reads the whole conversation and your CLAUDE.md. In my tests, cached re-reads were over 100× the output tokens.
- **Subagents have a startup cost.** Each one loads its own system prompt, tools and brief before doing any work.
- **Your main model matters most.** Usage limits are tracked per model, so running routine sessions on Sonnet stretches your usage further than any delegation rule. Switch with `/model`.

Results vary by task. Token counts in the video come from my own Claude Code session logs.
