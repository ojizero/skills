---
name: review
description: Review a change or artifact for problems it brings in, and report each one with evidence. Use when asked to review or look over a PR, diff, commit, plan, doc, or design.
license: MIT
---

Do one review pass and report claims. This pass is read-only: read and run checks as you need, but make edits, posts, or fixes only when the user asks for them. When the caller gives you a lane, such as security or one module, keep to it.

## Basis

1. **Pin** the exact basis: a commit SHA, a range, a diff, or a document version. Uncommitted changes, pasted text, or a live document have no fixed version. Review them as they are now, and say so in the report, with the time or the base commit. For a re-review, the basis is the range since the last reviewed version.
2. **State the intent:** what the change tries to do, in one or two lines, and its stage: who uses it today, and whether it is in production. Take these from the description, the issue, the commits, the decision records, or the artifact, and cite the source. When you infer them, say so. Current code and docs show what is, not always what is wanted: code that nothing calls yet can be unwired work, not dead code. Judge each claim against this intent.

## Fit

Before you read, set the pass from three facts: the stage of the review, the risk where a failure lands, and the kind of artifact. Take them from the request and the artifact, and state them in the report. When the caller's brief sets any of these, or the depth, the bar, or the format, the brief wins.

| Fact | Value | Pass |
|---|---|---|
| Stage | Draft or mid-build | Direction and structure only. Reading is enough. |
| | First review | Every changed part. Trace each claim. |
| | Re-review | The range since the last review. First check each earlier claim: fixed, still open, or settled. Settled claims stay closed. When the range is too large for a narrow pass, say so. |
| | Final | Confirm the earlier claims are fixed and the last changes broke nothing. |
| Risk | The failure reaches real data, money, secrets, health data, or a live machine | Run it: each claim on this path reaches `ran`, or says why it cannot. |
| Kind | Code | Concrete failures and simpler shapes. |
| | Doc or skill | Also wording that misleads its reader, such as a small model. `nitpick` claims count here. |
| | Idea, design, or research | Direction, boundaries, and fit, at the level the author works. Be bold, and leave code detail for later stages. |

Set depth by stage and risk. A large change gets the same bar as a small one, with more reading.

## Claims

A claim is a concrete failure that this change causes: "could be a problem" is not a claim, and a claim with no harm named gets the answer "And?". Aim for precision: a useless claim costs the reader more than a missed one, and a report with zero claims is a good result. Read every changed part of the basis against the intent. Keep a claim only when it passes each test:

- **Introduced:** this change adds or modifies the cause, makes an old problem worse, or touches or moves the code or text that holds it. Touched code is in scope.
- **Possible:** the inputs or state can occur, often enough to matter. A rare input with a small harm is out.
- **Not wanted:** the intent does not plan the result, and the change, the project, or the user does not already accept the risk.
- **Worth it:** the author would change something, or the reader would decide differently, because of it.

A real problem that fails only **Introduced** goes on the follow-ups list as one line with its location, not as a claim.

Write each claim to this standard:

- **Simpler shape:** for a structure or design claim, name the simpler shape that removes the problem (code judo), such as code to delete, a step to merge, or an option nobody needs.
- **Precise:** raise only what you are sure of. When you are not sure, check further or drop the claim. Label it `question` only when the answer decides whether something blocks, and say what you could not check.
- **Shown:** give the failing input or a short snippet, so the reader sees the cause and the effect without a second question.

Before you report, make a **cut**: read each claim as the author who must act on it, and delete each one that fails a test above. Merge claims that share one cause.

When other reviews exist, from bots or people, write your own claims first. Then read theirs. Add one of their points only when you confirm it with your own evidence.

## Confidence

Each claim states the highest level its evidence reaches:

1. **read:** you saw it in the code or text.
2. **traced:** you followed the path from the inputs to the failure.
3. **ran:** you reproduced it with a command, a test, or a run. When you can, give the minimum steps to reproduce it, such as a short test or command.

## Format

Each claim has these fields. Fit the format to where the report goes: a short list in a chat, a visual such as an HTML page or a diagram when it makes the claims faster to read, or structured data such as YAML or JSON when the caller asks for it. When the caller gives its own format, keep these fields inside it.

- **ID:** `C1`, `C2`, and so on, in report order, so the user can reply by ID.
- **Location:** path:line, or the section of the document.
- **Failure:** the inputs or state, and the wrong output, crash, or cost.
- **Evidence:** what you read, traced, or ran.
- **Confidence:** read, traced, or ran.
- **Label:** a Conventional Comments label: `issue`, `suggestion`, `question`, or `todo`, plus `nitpick` where the fit allows it. Add `blocking` or `non-blocking` when it changes what the reader must do. A `blocking` claim needs `traced` or `ran`.

Start the report with a short summary:

- **Counts:** how many claims, and how many of them are blocking.
- **Recommendation:** one line that starts with the action, by ID, such as "Fix C1 and C2 before merge; C3 can wait" or "Merge as is: only nitpicks". Recommend only: do not act on it.

Then give the basis, the intent, the fit, and the claims. For a re-review, give the status of each earlier claim before the new ones. Sort the claims by impact: blocking first, then by how bad the failure is and how much it reaches, such as how many users, callers, or paths. End with the follow-ups, if any. With no claims, say so, and list what you read.
