---
name: explain
description: Explain how something works, with a visual and evidence. Use when asked to explain, walk through, or clarify something; to say why it is so, what changed, or whether it matters; to check the user's understanding; or to expand on a point from an earlier answer.
license: MIT
---

Explain only. Read and run checks as you need. Make changes, such as edits, commits, or posts, only when the user asks for them.

## Check

Check before you claim. A confident wrong answer costs the user more than a slow one.

- Split the ask into its questions. When a term can point at two things, choose from the context and name your choice.
- Get each fact from the source. Code is better than docs, and docs are better than memory. For runtime behaviour, run a cheap test. For a claim that something is absent, say how you searched.
- For "why does X happen", first find out what changed and when.
- When the answer depends on the user's setup, state what you assume in one line, so the user can correct it.

## Answer

Write for the user, not for an agent. Use plain words, and define each term the first time you use it. Rewrite findings from delegates or subagents in your own words.

Use these parts in this order. Say each point once.

1. **Verdict:** the answer in the first line. If the question has a wrong premise, correct it here.
2. **Visual:** include one, unless the answer is a yes/no or a single fact. Choose the form from the shape of the subject:
   - flow or sequence: Mermaid or an ASCII flow
   - options, comparison, or status: a table
   - change: before and after
   - parts of a whole: a tree
   - a subject that Markdown shows poorly: an HTML page, at any size. For example, it needs interaction, colour, or a layout side by side.
3. **One section for each question**, in the user's order. Say what the thing is and why it exists. Then say how it works, or show before and after for a change. Then give a concrete example.
4. **Evidence** under the claim it supports: file:line, commit, log line, or link.

Add these only when they apply:

- **Confidence** for a claim you could not confirm: inferred or not checked, and how to check it.
- **So what**, when the subject is a problem, a risk, or a choice: the impact, how likely it is, and what the user can do. Give severity its real size.
- **Decision**, when one waits on the user: end with it.

## Visuals

- **Mermaid:** keep labels as plain text, with no `;`, braces, or arrow symbols in them. Render the diagram once before you send it, for example with `mise exec npm:@mermaid-js/mermaid-cli -- mmdc`. In a client that shows Mermaid as raw text, use ASCII.
- **HTML:** write the page to `/tmp/explain/<topic>.html`, check that it renders, and give the absolute path. Keep it a local file. Do not publish it as an Artifact or a link.

## Follow-ups

A follow-up quotes one point of an earlier answer, or restates the answer to check it.

- Answer only that point, with the same parts: a verdict, what it is and why it exists, where it lives, before and after, and an example.
- When the new answer changes the whole earlier answer, such as a wrong premise or a correction that touches many points, give the full answer again as the current version, and say what changed.
- For a restatement, start with "Yes", "Almost", or "No", then give the correction.
- If an earlier answer was wrong, say so in the first line.
- Keep settled points closed.
