---
name: shepherd
description: Keep one or more threads, sessions, or agents on track to a goal while they own the plan, the work, and how they work together. Not for splitting work or combining results.
license: MIT
disable-model-invocation: true
metadata:
  status: testing
---

The workers own the plan, the work, and how they work together. You keep them on course to the goal. Use babysit to wait and finish.

A worker is a thread: a running agent that you can read from a mark and send a message to. Examples are a T3 Code thread, a Claude Code session, and a peer agent. A subagent or delegate is part of the thread that started it. Watch that thread, not the subagent.

## Charter

- **Goal:** the end state, in the user's words.
- **Done:** the milestone that ends this watch, often the goal itself.
- **Workers:** each thread's exact ID, what it owns, and your mark: where you last read it.
- **Limits:** actions left to the user or the workers, and whether you may restart a worker.
- **Decisions:** the user's rulings and corrections, word for word. Pass each one to the workers it affects.

Read every charter change back to the user in one line. When the watch outlives your turn, keep the charter in a temporary file and read it at each check.

## Each check

Read each worker from its mark. Judge it from current evidence you inspect yourself: the diff, the artifact, the run record, newer than the last change that could affect it. A worker's report is a claim to check. Label each worker:

- **progressing:** a new result since the mark: a commit, artifact, finding or decision. Running is not progress.
- **waiting:** blocked on something that must finish first. Record what, and what ends the wait.
- **stalled:** no new result, waiting on what need not block, or repeating.
- **drifting:** working outside the charter, or leaving out part of the goal it should be on by now.

Nudge a stalled worker with the evidence and its next step. Redirect a drifting one to the charter. After two ignored nudges, find what blocks it. If the limits allow restarts, stop the worker and start a fresh thread from a handoff you write from the charter and the evidence; otherwise tell the user.

The check is complete when done is tested, every worker is labelled, every mark is updated, and every stalled or drifting worker is handled.

## The user's contact

Carry out the user's orders to the workers within the limits. Answer status questions read-only: inspect the evidence first, and cite what each worker did and when.
