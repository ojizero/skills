---
name: review
description: Review a change or artifact and report claims. Use when asked to review, look over, or check a PR, diff, commit, plan, doc, or design.
license: MIT
---

Do one review pass and report claims. This pass is read-only: read and run checks as you need, but make edits, posts, or fixes only when the user asks for them. When the caller gives you a lane, such as security or one module, keep to it.

## Basis

1. **Pin** the exact basis: a commit SHA, a range, a diff, or a document version. Uncommitted changes, pasted text, or a live document have no fixed version. Review them as they are now, and say so in the report, with the time or the base commit.
2. **State the intent:** what the change tries to do, in one or two lines. Take it from the description, the issue, the commits, or the artifact, and cite the source. When you infer it, say so. Judge each claim against this intent.

## Claims

A claim is a concrete failure that this change causes: "could be a problem" is not a claim. Read every changed part of the basis against the intent. Keep a claim only when it passes each test:

- **Introduced:** this change adds or modifies the cause, or makes an old problem worse. A problem that was there before is out.
- **Possible:** the inputs or state can occur.
- **Not wanted:** the intent does not plan the result, and the change, the project, or the user does not already accept the risk.

Write each claim to this standard:

- **Simpler shape:** for a structure or design claim, name the simpler shape that removes the problem (code judo), such as code to delete, a step to merge, or an option nobody needs.
- **Precise:** raise only what you are sure of. When you are not sure, label it `question` and say what you could not check. Few true claims are better than many weak ones.

When other reviews exist, from bots or people, write your own claims first. Then read theirs. Add one of their points only when you confirm it with your own evidence.

## Confidence

Each claim states the highest level its evidence reaches:

1. **read:** you saw it in the code or text.
2. **traced:** you followed the path from the inputs to the failure.
3. **ran:** you reproduced it with a command, a test, or a run. When you can, give the minimum steps to reproduce it, such as a short test or command.

## Format

Each claim has these fields. Fit the format to where the report goes: a short list in a chat, a visual such as an HTML page or a diagram when it makes the claims faster to read, or structured data such as YAML or JSON when the caller asks for it.

- **Location:** path:line, or the section of the document.
- **Failure:** the inputs or state, and the wrong output, crash, or cost.
- **Evidence:** what you read, traced, or ran.
- **Confidence:** read, traced, or ran.
- **Label:** use a Conventional Comments label, such as `issue`, `suggestion`, `nitpick`, `question`, `todo`, `thought`, or `praise`. Add `blocking` or `non-blocking` when it changes what the reader must do.

Report the basis, the intent, and then the claims, most severe first. With no claims, say so, and list what you read.
