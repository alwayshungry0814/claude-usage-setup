# Claude Usage Setup Prompt

One prompt for **Claude Code** (terminal, desktop app or IDE, run locally) that sets up your global `CLAUDE.md` to get the best results for the least usage: when to orchestrate, which subagents to run, how much effort to spend, and how to keep context small.

▶️ Watch the video: **[2x your Claude Usage](https://youtube.com/shorts/c_46bmZoDmE)**

From the video: In my tests, Opus alone matched Opus + Haiku subagents on a simple build while using a fraction of the tokens. Subagents only paid off on big, parallel search work. The rule: the task has to justify the orchestrator.

## How to use it

1. Open Claude Code on your own computer. Cloud sessions on claude.ai/code don't keep your global settings.
2. Paste the prompt below.
3. Review the diff Claude shows you, then let it save.
4. Make the three changes it recommends that only you can make (model, effort, connectors).

## The prompt

```
Set up my global CLAUDE.md (~/.claude/CLAUDE.md) to get me the best results for the least usage. Work cheaply while doing this.

1. Audit my setup: list my connected MCP servers/connectors (e.g. `claude mcp list`) and, by searching my recent session logs for "mcp__<server>__" tool names, flag the ones I haven't used. Also remind me to check connectors added in the Claude app or claude.ai settings, which that command doesn't list. Their tool definitions load into every request. Recommend only; don't disconnect anything.

2. Review how I use you: with a script (don't read whole files), extract my own prompts (user messages, first 300 characters each) from my 20 most recent sessions in ~/.claude/projects/. Have a Haiku subagent summarize my common task types in 5 bullets. If I have fewer than 5 sessions, skip this and use the defaults below.

3. Merge the block below into my CLAUDE.md. Tune only the thresholds and examples to my task types; keep the rules and keep it under 30 lines. Keep everything already in the file; merge rather than duplicate. If an existing rule conflicts with this block, show me both and ask which to keep. Project-level CLAUDE.md files take priority over this one.

## Usage (best results, least usage)
Priority: correct results > my time > tokens. Never trade correctness for savings.

Context (the biggest cost; every turn re-reads it):
- Search first, then read only the lines you need. Don't re-read files you already have.
- Don't paste long logs or whole files into replies; summarize and cite paths.
- Prefer text tools over screenshots.
- Keep replies short: lead with the answer, skip recaps.
- Tell me when a fresh session (/clear) or /compact would help.

Rework (the second biggest cost):
- If a request is ambiguous in a way that changes the result, ask one question first.
- For multi-step changes, state a short plan first.
- Run the narrowest test that proves a change; run the full suite once at the end.

Subagents (the task has to justify the orchestrator):
- Default: do the work yourself. No subagents for small, sequential or tightly coupled work.
- Delegate only for 3+ independent pieces or broad reading/search (10+ files or sources), where each piece can come back as a short summary.
- Models: Haiku for search, reading, summaries and running tests; Sonnet for real coding; Opus only if the others would fail (tell me).
- Effort: run subagents at low or medium effort unless the piece is hard.
- Briefs: standalone, with acceptance criteria and a summary of at most 15 lines (file paths, not dumps). Launch independent ones in parallel, at most 5 unless I ask.
- Verify results. If a subagent fails once, finish it yourself or move up one model; don't retry the same brief.
- Keep "one best answer" work (design, hard debugging, final review) in the main session.
- Tell me when a task would be fine on Sonnet or at lower effort, or needs higher effort.

4. Show me the diff before saving.

5. Finish with the 3 changes only I can make: my default model (Sonnet for routine work, Opus for hard work), my effort level, and which connectors to disconnect. Mention a setting only if my plan and Claude Code version have it.
```

## Why these rules

- **Context is the biggest cost.** Every turn re-reads the whole conversation, your CLAUDE.md and the definitions of every connected tool. In my tests, cached re-reads were over 100× the output tokens.
- **Subagents have a startup cost.** Each one loads its own system prompt, tools and brief before doing any work: tens of thousands of tokens, depending on your tools.
- **Rework is expensive.** A wrong guess that has to be redone costs more than any setup choice.
- **Your main model matters most.** Usage limits are tracked per model, so running routine sessions on Sonnet stretches your usage further than any delegation rule. Switch with `/model`.

## Measure it

Note your 5-hour and weekly usage over a typical week before and after. Results vary by task; token counts in the video come from my own Claude Code session logs.

## License and disclaimer

Released under the [MIT License](LICENSE).

This prompt and its rules are provided "as is," without warranty of any kind. Results, token counts and usage savings vary by task, plan, model and Claude Code version, and nothing here guarantees them. The prompt asks Claude Code to edit your global `CLAUDE.md` and read your local session logs. Review every change before you accept it, and back up your settings first. You are solely responsible for how you use it. To the fullest extent permitted by law, the author is not liable for any loss of data, usage, money or other damages arising from its use.

This is an independent project. It is not affiliated with, endorsed by or sponsored by Anthropic. Claude and Claude Code are trademarks of Anthropic.
