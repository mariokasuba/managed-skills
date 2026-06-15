---
name: list-files
description: "List files in the current directory."
version: 0.2.0
author: Hermes user
license: MIT
platforms: [linux, macos, windows]
---

# List Files

Use `search_files` for file discovery across the workspace, or `terminal` for an explicit directory listing. Use `read_file` to inspect a file after selecting it.

## Default behavior
When the user just asks to list or inspect the current directory contents, return a concise listing first:
- Prefer `search_files(target='files', path='.', limit=200)` for normal populated directories.
- For empty output, check the current working directory and common top-level paths.

## Steps
1. Determine the working directory when the user references "here" or "current directory".
2. Run `search_files(target='files', path='.', limit=200)` and present results.
3. If `read_file` fails with file-not-found, re-run `search_files` to confirm the path.
4. If the output is still empty, infer common candidate paths and check them.

## Guardrails
- Do not recurse outside the requested directory unless explicitly asked.
- Keep output concise; avoid dumping trees unless requested.
