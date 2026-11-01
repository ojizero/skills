---
name: babysit
description: Watch work until it is done, and act on what comes up. Use when asked to watch, monitor, or babysit something, or to keep going until it is green or done.
license: MIT
---

Stay with the work until it is done. The user must not have to tell you to continue.

## Contract

Get these from the user's request or the current context:

- **Target:** what you watch.
- **Done:** a state you can check, such as "all checks pass and no review thread is open".
- **Then:** the action after done, if any, such as a merge.
- **Limits:** what you must not touch.

Tell the user the contract in one or two lines. If the target or done is not clear, ask. Do not guess: the user must trust that you watch the right thing.

## Loop

1. **Wait** on a wake-up that is in place: an event watch, a background command that wakes you, or a scheduled task for work that runs longer than your turn. Do not say you will check later unless something will wake you. If a watch times out, arm it again.
2. **Check** every source against done. Check the result, not a sign of it: a run that ended is not done if its report did not publish.
3. **Act** inside the contract. Fix what is in scope, and retry a temporary error a few times. Do not start, stop, or restart work the contract does not cover. When you need the user, say what you need in one line, and keep the watch in place.
4. **Report** a short status at each milestone, then wait again.

## Finish

When done holds, or only the user can move the work forward, remove the watches and scheduled tasks you set up. Then report where the work is, what you changed, and what waits on the user.
