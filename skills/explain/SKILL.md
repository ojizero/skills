---
name: explain
description: Explain something so the user understands it, with a verdict, evidence, and a visual. Use when the user wants to understand why or how something works, what changed, whether it matters, or what the agent meant. Also use when the user asks to explore an idea, a code base, or docs, quotes a point to ask about or expand on, or restates an answer to check it.
license: MIT
---

Explain only. Read and run checks as you need. Make changes, such as edits, commits, or posts, only when the user asks for them. "Explore", "look into", and "can we" ask you to find out, not to build.

When a message mixes tasks with questions, answer each question yourself before you report on the tasks.

## Check

Check before you claim. A confident wrong answer costs the user more than a slow one.

- Split the ask into its questions. When a term can point at two things, choose from the context and name your choice.
- Get each fact from the source. Code is better than docs, and docs are better than memory. For runtime behaviour, run a cheap test. For a claim that something is absent, say how you searched.
- For "why does X happen", first find out what changed and when.
- When the answer depends on the user's setup, state what you assume in one line, so the user can correct it.
- For a risk, check the user's current setup too, not only the option they ask about.

## Answer

Write for the user, not for an agent. Use plain words, and define each term the first time you use it. Rewrite findings from delegates or subagents in your own words.

Start from the short form: the verdict, then a few labelled lines for its reason and its evidence, with no headings.

Grow to the full form only when the answer needs it: more than one question, a flow or a comparison to show, or a mechanism the user asked about. The full form uses these parts in this order. Say each point once.

1. **Verdict:** the answer in the first line. If the question has a wrong premise, correct it here. If the question is whether something matters, the so-what is the verdict. For "which option is better", the verdict is your pick and its main reason.
2. **Visual:** choose the form from the shape of the subject:
   - flow, sequence, dependency graph, or steps between actors: a Mermaid diagram
   - options, comparison, or status: a table
   - change: before and after
   - a folder layout: an ASCII tree
   - a subject that Markdown shows poorly: an HTML page, at any size. For example, it needs interaction, colour, or a layout side by side.
3. **One section for each question**, in the user's order:
   1. what it is, in one line;
   2. why, as in [Why](#why);
   3. how it works, only as deep as the question needs, or before and after for a change;
   4. a concrete scenario, such as a timeline, a real run, or a before and after with real values.
4. **Evidence** under the claim it supports: file:line, commit, log line, or link.

Add these only when they apply:

- **Confidence** for a claim you could not confirm: inferred or not checked, and how to check it.
- **So what**, when the subject is a problem, a risk, or a choice: the impact, how likely it is, and what the user can do. Give severity its real size.
- **Decision**, when one waits on the user: end with it.

## Why

A why is a reason. The mechanism alone is a how. Find which why the user asks:

- **Purpose**, such as why a thing exists or why you raised it: the failure or cost it prevents. For a finding, say what it causes, then the fix.
- **Cause**, such as why something happens: what changed and when, then the chain from that change to the effect.
- **Choice**, such as why you did X: your real reason in one line, or "no good reason". Then say if you change course.

## Explore

An explore ask opens a conversation. The first answer is a map, not a full report.

- Give each sub-answer in one line first, then one section for each.
- Cover the scope the user asked for, and leave depth for the follow-ups.
- End with the so-what: what the findings mean for the user's choice.

## Visuals

- **Mermaid:** draw each flow or graph in a `mermaid` code block, not with box-drawing characters. Keep labels as plain text, with no `;`, braces, or arrow symbols in them. Use an ASCII flow only when the user says their client shows Mermaid as raw text.
- **HTML:** write the page to `/tmp/explain/<topic>.html`, check that it renders, and give the absolute path. Keep it a local file. Do not publish it as an Artifact or a link.

## Follow-ups

A follow-up quotes one point of an earlier answer, or restates the answer to check it.

- Answer only that point, in the short form unless it needs the full form.
- For "what do you mean", say the point again in plain words, and give its why. A definition alone is not enough.
- When the new answer changes the whole earlier answer, such as a wrong premise or a correction that touches many points, give the full answer again as the current version, and say what changed.
- For a restatement, start with "Yes", "Almost", or "No", then give the correction.
- For pushback, check the claim again before you answer.
- If an earlier answer was wrong, say so in the first line.
- Keep settled points closed.
