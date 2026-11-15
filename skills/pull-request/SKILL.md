---
name: pull-request
description: Open, write, or check a pull request. Use when the intent is to make, edit, or check the state of a PR.
license: MIT
---

Describe the net change of the branch against its base, including commits from other sessions or people. Describe what the change is, not how it got there.

## Title

The title becomes the merge subject, so it must stand alone. Follow the commit subject style in `git log`. With no clear style, use Conventional Commits.

## Description

```markdown
## Why

## What changed

## Evidence

## Merge danger

**Door:** <one-way | two-way>: <why>
**Blast radius:** <area>: <who or what it affects>

## Review notes
```

- **Why:** the problem or the motivation, in one to three sentences. Say what the PR does only when the title does not. Link the related issues in the syntax of their tracker, such as `Closes #<n>` or a ticket key.
  - Take the issues from the context first: the request, the branch name, the commits, or the session.
  - With none in the context, search the project's trackers for open issues. Link an issue only when you are sure it describes the problem this change solves.
- **What changed:** the behaviour, not a list of files. When a visual makes the change clearer, lead with the smallest one:
  - Mermaid for a flow or an interaction.
  - A tree for structure: files, components, or calls.
  - A `diff` sketch when the structure exists and changes.
- **Evidence:** what you ran and what it showed. Show before and after where you can.
- **Merge danger:**
  - **Door:** one-way when a revert cannot undo the change, such as a migration, a data write, a message or delivery sent, or a removed API that clients use. Two-way otherwise.
  - **Blast radius:** one word for the area, then who or what it affects.
- **Review notes:** only points that need a reviewer's decision or a slow read. Leave the section out when there are none.

Keep it short: a reviewer must get it in under a minute. The detail lives in the commits and the diff. The description says what the PR is now. Put its history in comments.

## Terms

- **Synced:** the latest commits of the base are merged in, with no conflicts.
- **Green:** every required check passed. None is pending.
- **Answered:** every review thread has a fix or a reply, and is resolved.
- **Ready:** green, answered, and free of conflicts. Only a human approval may still be pending.
