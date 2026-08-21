---
name: pr-create
description: Create a new pull request.
disable-model-invocation: true
license: MIT
---

Open a pull request with `gh` for the current branch against the repo default branch, once the current branch is clean: everything committed and pushed.

## Steps

1. Check `gh auth status`. On failure, stop and say what failed — `gh` is the only path here, so there is no workaround to reach for.
2. Check the current branch against the repo default branch. If they are the same, tell the user this skill needs a topic branch and stop — leave the branch and the work as they are.
3. Commit and push until the branch is clean — `git status` shows nothing to commit, and the branch tracks a remote with nothing ahead of it.
4. Account for the whole change. Start from what this session already holds — the work you just did needs no re-reading. Then close the gaps with `git diff <default>...HEAD --stat` and the commit subjects, so work from before this session, or from another author, is covered too. Read the full diff only where the summary leaves you guessing at what a change does.
5. Read the repo's conventions: `git log --oneline -30` for the commit subject pattern, and any pull request template under `.github/`.
6. Write the title and the description by the rules below, then run `gh pr create`.

## Title

The title lands in the Git history as the subject of the merge, so it names the work done well enough to stand alone years later.

Follow the subject pattern the log shows. When the log shows no pattern, write a Conventional Commits subject.

## Description

Open with an attribution note, above the parts and outside any section: the harness, the model and its version, the provider, and the session ID, on one line, so a reader sees that an agent opened this pull request, and which one.

> _Opened by Claude Code · claude-opus-5 (Anthropic) · session `01ab…`_

Write the fields this session already holds, and drop the note when it holds none — none of them is worth digging for.

Then four parts, in order:

1. **Intention** — one sentence on what this change does.
2. **Problem** — the plain statement of what is wrong or missing today.
3. **Solution** — how the change answers that problem.
4. **Validation** — the checks you ran, and their results.

Write it in ASD-STE100: short sentences, one idea each, active voice, common words, and the terms this codebase already uses. Keep to facts — what changed, and what you verified.
