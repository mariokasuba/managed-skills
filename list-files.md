---
name: list-files
description: "List files in the current directory."
version: 0.3.0
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

## Tabular overview
Always present directory contents as a Markdown table with the following columns:

| Column        | Description                                       |
|---------------|---------------------------------------------------|
| **Name**      | File or directory name (directories suffixed `/`) |
| **Type**      | `file` or `dir`                                   |
| **Size**      | Human-readable size (e.g. `4.2 KB`, `1.1 MB`)    |
| **Modified**  | Last-modified date in `YYYY-MM-DD` format         |

### Example output

| Name              | Type | Size    | Modified   |
|-------------------|------|---------|------------|
| src/              | dir  | —       | 2025-06-10 |
| README.md         | file | 3.2 KB  | 2025-06-12 |
| package.json      | file | 1.1 KB  | 2025-06-11 |
| dist/             | dir  | —       | 2025-06-09 |

- Directories show `—` for size.
- Sort: directories first, then files, both groups alphabetically.
- If modified date is unavailable, show `—`.

## Guardrails
- Do not recurse outside the requested directory unless explicitly asked.
- Keep output concise; avoid dumping trees unless requested.
- Always format file sizes in human-readable units (B, KB, MB, GB) — never raw byte counts.
- Never output machine-only formats (JSON, raw stat output) unless explicitly requested.