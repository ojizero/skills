---
name: refute
description: Try to break claims, such as review findings or bot comments, against the source, and report which ones hold. Use when asked to refute, verify, or challenge findings or review comments, or to check if they are real.
license: MIT
---

Try to break each claim. A claim is wrong until the evidence shows that it holds.

Refute only. Read, and run cheap throwaway checks in a scratch or temporary folder to reach the highest confidence that costs little. Leave the code, the claims, and their threads as they are: make fixes, edits, or posts only when the user asks for them.

## Basis

1. **Pin** the exact basis: the commit, range, diff, or document version that the claims are about. Uncommitted changes, pasted text, or a live document have no fixed version. Check them as they are now, and say so in the report, with the time or the base commit.
2. **Read each claim** into its location, its failure (the inputs or state, and the wrong result), its evidence, and its label. Claims come in any shape, so infer the parts that are not stated. When you cannot tell what fails, say so in the verdict.

## Check each claim

Check each claim on its own. The verdict on one claim does not carry to another, even from the same source.

- **Go to the source.** Read the code or artifact at the basis. Build your own reasoning. The claim's quoted code can be stale, partial, or from another file.
- **Test the premise:**
  - **Possible:** can the inputs or state occur? Follow them back to where they enter. A guard, a validation, a type, or a constraint elsewhere can stop them before they reach the failure. For example, data that is validated on entry never reaches a parser in a malformed state. Search for that one fact. When you find none, say how you searched.
  - **Introduced:** did this change bring it in, or make an old problem worse? A problem that was there before is out.
  - **Not wanted:** the change does not mean to cause the result, and the change, the project, or the user does not already accept the risk. Look for tests, docs, comments, or recorded decisions that say so.

## Confidence

Each verdict states the highest level its evidence reaches:

1. **read:** you saw it in the code or text.
2. **traced:** you followed the path from the inputs to the failure.
3. **ran:** you reproduced it with a command, a test, or a run. When you can, give the minimum steps to reproduce it, such as a short test or command.

## Verdicts

- **holds:** the failure happens as claimed.
- **holds in part:** only part of the claim holds. Narrow the failure to that part.
- **fails:** the evidence breaks the claim. Give the fact that breaks it.

Merge claims that share one root cause into one verdict.

Keep the label, or lower it when the evidence shows a smaller impact, such as `issue` to `suggestion` or `blocking` to `non-blocking`. Never raise it. A new problem that you find while you refute is not a verdict: put it under Notes, for a new review.

## Format

Start the report with a short summary:

- **Counts:** how many claims hold, hold in part, and fail.
- **Recommendation:** one line that starts with the action, by ID, such as "Fix C1 and C3; C2 can wait; drop the rest" or "Merge as is: no blocking claim holds". Recommend only: do not act on it.

Then give one verdict for each claim or merged group, in input order. Keep every claim, including each one that fails, so the reader sees what was dropped and why. Fit the format to where the report goes: a short list in a chat, a visual such as an HTML page or a diagram when it makes the verdicts faster to read, or structured data such as YAML or JSON when the caller asks for it.

- **Claim:** the claim's ID, such as `C1`, or the IDs you merged. Keep the IDs that the claims have. When they have none, give them `C1`, `C2`, and so on, in input order.
- **Verdict:** holds, holds in part, or fails.
- **Evidence:** what you read, traced, or ran.
- **Confidence:** read, traced, or ran.
- **Label:** the label, and the label it had before when you lowered it.

End with Notes: new problems for a new review, each with an ID such as `N1`, a location, and a failure. Leave Notes out when there are none.
