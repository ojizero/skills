---
name: pr-babysit
description: Monitor and babysit a pull request until it's mergeable.
disable-model-invocation: true
license: MIT
---

Watch a pull request with `gh` until it is **green and answered**: every check passes, and every review comment holds a fix or a refutation.

The work is a cycle of sweep, act, wait. Repeat it until the exit bar is met. A push resets the cycle, because it voids the last green and invites new comments.

## Steps

1. Check `gh auth status`. On failure, stop and say what failed. `gh` is the only path here, so there is no workaround to reach for.
2. Find the pull request: the number the user named, or `gh pr view --json number,headRefName` for the current branch. With no pull request, stop and tell the user.
3. Place the work on the head branch, so a fix lands on the right branch and the branch you started on stays as it is. An instruction from the user wins here. Otherwise take the first case that holds:
   - The current branch is the head branch. Work in place.
   - A worktree in `git worktree list` holds the head branch. Work in it.
   - Neither. Make one: `git fetch origin <head>`, then `git worktree add ../<repo>-pr-<number> <head>`. Remove it with `git worktree remove <path>` when you stop, on any exit.
4. Read the repo's commit subject pattern: `git log --oneline -30`.
5. Sweep (see [Sweep](#sweep)).
6. Act on everything the sweep found. Fix or refute each open comment, and repair each failing check and each conflict.
7. Wait for the checks: `gh pr checks --watch`. This blocks until every check finishes, so the wait costs no polling.
8. Sweep again. Stop when the sweep comes back green and answered, else return to step 6.

## Sweep

Read all three sources every cycle. Each one holds work the others hide.

**Checks.** `gh pr checks`. For a failure, read the log with `gh run view <run-id> --log-failed`.

**Review threads.** One GraphQL query, because `gh pr view --comments` drops inline review comments and carries no resolved state.

```
gh api graphql -f query='
  query($owner:String!, $repo:String!, $pr:Int!) {
    repository(owner:$owner, name:$repo) { pullRequest(number:$pr) {
      reviewThreads(first:100) { nodes {
        id isResolved path line
        comments(first:20) { nodes { databaseId author { login } body } }
      } } } }
  }' -F owner=OWNER -F repo=REPO -F pr=NUMBER
```

**Merge state.** `gh pr view --json comments,reviews,reviewDecision,mergeable,mergeStateStatus`. This holds the top-level discussion, the review verdicts, and any conflict.

## Fix or refute

Read the code the comment names before you judge it. Then take one of two branches.

**Fix.** The comment finds real work. Change the code, commit in the repo's subject style, and push. Reply with the commit SHA.

**Refute.** The comment asks for work that is wrong, or already done. Reply with the reason: what the code does, and why the comment does not apply. A comment that only asks a question gets its answer here.

Both branches end the same way. Post the reply, then resolve the thread.

```
gh api repos/OWNER/REPO/pulls/NUMBER/comments/COMMENT_ID/replies -f body='...'
gh api graphql -f query='mutation($id:ID!){ resolveReviewThread(input:{threadId:$id}){ thread { isResolved } } }' -F id=THREAD_ID
```

Use `gh pr comment` to answer a top-level comment.

A conflict is work of the same kind. Rebase or merge the default branch, fix the conflict, and push.

## Comments

Every comment you post opens with an attribution note, above the body: the harness, the model and its version, the provider, and the session ID, on one line, so a reader sees that an agent wrote this comment, and which one.

> _Posted by Claude Code · claude-opus-5 (Anthropic) · session `01ab…`_

Write the fields this session already holds, and drop the note when it holds none. None of them is worth digging for.

Write the body in ASD-STE100: short sentences, one idea each, active voice, common words, and the terms this codebase already uses. Keep to facts: what the code does, what you changed, and what you verified. One comment carries one point.

## Green and answered

The exit bar. Every part holds:

- `gh pr checks` shows every check passed. No check is pending, and none failed.
- Every review thread reads `isResolved: true`.
- `mergeable` reads `MERGEABLE`.
- The branch is clean. `git status` shows nothing to commit, and nothing ahead of the remote.

Then report the final state to the user.

A pull request can meet the bar and still wait on a human, for an approval, or on a `CHANGES_REQUESTED` verdict with no comment left to answer. That pull request is done for you. Say what it waits on, and stop.
