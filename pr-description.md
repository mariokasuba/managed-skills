---
name: pr-description
description: "Generate a clear, structured pull request description from staged changes or a summary of work done."
version: 0.1.0
author: Itera
license: MIT
platforms: [linux, macos, windows]
---

# PR Description

Generate a well-structured pull request description when the user asks to create or draft a PR description, commit message summary, or merge request body.

## Steps

1. Ask for (or read from context): the list of changed files, a short summary of what changed, and the motivation.
2. Produce a description with these sections:
   - **What** – one-sentence summary of the change.
   - **Why** – motivation or problem being solved.
   - **How** – brief implementation notes (optional for small changes).
3. Keep the tone concise and factual.

## Example output

```
## What
Replace HTTP polling with WebSocket connection for real-time notifications.

## Why
Polling caused excessive server load and 2–5 s latency on updates.

## How
Added `NotificationHub` (SignalR) and replaced `setInterval` fetch loop in `NotificationsService`.
```

## Guardrails

- Do not invent file names or changes not mentioned.
- Keep total length under 300 words.
