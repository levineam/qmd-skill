---
name: qmd
description: Local hybrid search for markdown notes and docs. Use when searching notes, finding related content, or retrieving documents from indexed collections.
homepage: https://github.com/tobi/qmd
metadata: {"clawdbot":{"emoji":"🔍","os":["darwin","linux"],"requires":{"bins":["qmd"]},"install":[{"id":"bun-qmd","kind":"shell","command":"bun install -g https://github.com/tobi/qmd","bins":["qmd"],"label":"Install qmd via Bun"}]}}
---

# qmd - Quick Markdown Search

Local search engine for Markdown notes, docs, and knowledge bases. Index once, search fast.

## When to use (trigger phrases)

- "search my notes / docs / knowledge base"
- "find related notes"
- "retrieve a markdown document from my collection"
- "search local markdown files"

## Prerequisites

- Bun >= 1.0.0
- macOS: `brew install sqlite` (SQLite extensions)
- Ensure PATH includes: `$HOME/.bun/bin`

Install Bun (macOS): `brew install oven-sh/bun/bun`

## Install

`bun install -g https://github.com/tobi/qmd`

## Setup

```bash
qmd collection add /path/to/notes --name notes --mask "**/*.md"
qmd context add qmd://notes "Description of this collection"  # optional
qmd embed  # one-time to enable vector + hybrid search
```

## Search modes

- `qmd search`: fast keyword match (BM25)
- `qmd vsearch`: semantic similarity (vector)
- `qmd query`: hybrid search + reranking (best quality, slower)

## Common commands

```bash
qmd search "query"
qmd vsearch "query"
qmd query "query"
qmd search "query" -c notes     # Search specific collection
qmd search "query" -n 10        # More results
qmd search "query" --json       # JSON output
qmd search "query" --all --files --min-score 0.3
```

## Useful options

- `-n <num>`: number of results
- `-c, --collection <name>`: restrict to a collection
- `--all --min-score <num>`: return all matches above a threshold
- `--json` / `--files`: agent-friendly output formats
- `--full`: return full document content

## Retrieve

```bash
qmd get "path/to/file.md"       # Full document
qmd get "#docid"                # By ID from search results
qmd multi-get "journals/2025-05*.md"
qmd multi-get "doc1.md, doc2.md, #abc123" --json
```

## Maintenance

```bash
qmd status                      # Index health
qmd update                      # Re-index changed files
qmd embed                       # Update embeddings
```

## Models and cache

- Uses local GGUF models; first run auto-downloads them.
- Default cache: `~/.cache/qmd/models/` (override with `XDG_CACHE_HOME`).
