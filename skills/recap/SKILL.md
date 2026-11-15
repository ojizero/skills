---
name: recap
description: Catch the user up on a thread or project after a gap, with what was decided, what is done and open now, and the next step. Use when asked to recap or catch up, for the status, or for what is left or what is next.
license: MIT
---

Catch the user up so they can act at once. Assume the user remembers the goal and little after it.

Recap only. Read and check, and change nothing until the user asks.

## Scope

Take the scope from the user's prompt and the current context: this thread, the threads or links that the user names, or a project. Follow each named thread to where it lives, also on other machines.

## Gather

1. **Read the history newest first.** Then go back to each decision point. Long or compacted threads can show the oldest items first: page from the end.
2. **Read the work records** that the scope names or that the project's instructions point to, such as plans, decision logs, and notes.
3. **Check each past status against the live state now:** git (branch, commits, ahead or behind, uncommitted changes), pull requests, tests, and running systems. A past status is a claim, also when an earlier agent wrote it. Mark each fact that you could not check as **stale**.

The gather is done when each item that you report has evidence from now or a stale mark.

## Reply

Keep it short. Give the sections in this order, and leave out a section that has nothing in it:

1. **Verdict:** one line. Is the work done, open, or blocked, and on what?
2. **Decided:** the decisions that still hold, each with its source.
3. **Since last time:** what closed or moved after the history stopped, with evidence.
4. **Open:** a table of item, state, why it matters, and where (file:line, commit, pull request, or thread link). For state, use one of: `planned`, `in flight`, `uncommitted`, `open PR`, `merged`, `blocked`, `stale`.
5. **Deferred:** the items put off on purpose, and why.
6. **Your calls:** only the decisions that the user alone can make.
7. **Next step:** the one most useful action.

End with one question at most.
