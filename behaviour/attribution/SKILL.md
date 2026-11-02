---
name: attribution
description: Sign messages you post on the user's behalf. Use before you send anything other people will read, such as a PR, comment, issue, chat message, or email.
license: MIT
---

Start the message with one line that tells the reader an agent wrote it, and which one. Set the line apart from the body: a quote block (`>`) in Markdown, or the nearest equivalent elsewhere.

> _<Verb> by <harness> via <app> · <model> (<provider>)_

For example, with an app and without one:

> _Posted by Codex via T3 Code · gpt-6.1 (OpenAI)_

> _Opened by Claude Code · claude-opus-5 (Anthropic)_

- **Verb:** one past-tense verb that says what you did, such as _Opened_, _Posted_, _Sent_, _Updated_, _Reviewed_, or _Fixed_. Choose another when it fits better.
- **Fields:** fill in what this session holds, and drop the rest. Do not dig for them. With none, write _<Verb> by an agent_.
- **Edits:** keep the lines already there. Add yours below them, as a new paragraph in the same quote block.

Output already known to be agentic, such as code, docs, or a folder of AI-only files, gets no line.
