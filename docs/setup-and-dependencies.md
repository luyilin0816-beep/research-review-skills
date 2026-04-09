# Setup and Dependencies

## Overview

This repository assumes a local research workflow rather than a cloud-only workflow. It was designed around:

- browser-assisted literature search
- local Zotero usage
- local Obsidian usage
- NotebookLM as a module-writing assistant

## Core dependencies

### Required

- Codex with local skills enabled
- Chrome or an equivalent browser automation target
- Zotero
- Obsidian
- access to CNKI
- access to Google Scholar
- access to NotebookLM

### Strongly recommended

- a Zotero MCP or equivalent Zotero automation path
- an Obsidian CLI workflow
- a browser automation layer such as Chrome MCP or a reusable web-access layer

## Dependency checklist by workflow stage

### Stage 1: keyword calibration, search, PDF retrieval, and Zotero ingest

The public `research-review-01-keyword-calibration-search` skill assumes the following helper skills or equivalent capabilities:

- `cnki-search`
- `cnki-advanced-search`
- `cnki-parse-results`
- `cnki-paper-detail`
- `cnki-download`
- `cnki-navigate-pages`
- `gs-search`
- `gs-advanced-search`
- `gs-cited-by`
- `gs-fulltext`
- `web-access` or an equivalent browser automation path

It also assumes one stable Zotero integration path:

- Zotero MCP, or
- a local Zotero connector, or
- another verified local Zotero automation path

And one stable Obsidian note output path:

- Obsidian CLI, or
- another equivalent note-writing automation layer

### Stage 2: module framing, NotebookLM prompts, and source upload

The public `research-review-02-notebooklm-prompts-execution` skill assumes:

- access to NotebookLM
- a visible browser automation path for NotebookLM interaction
- one stable way to locate local PDFs from the approved paper set
- one stable Zotero lookup path if source files are stored through Zotero

Recommended helpers:

- `web-access`
- Zotero MCP or equivalent Zotero lookup automation

### Stage 3: NotebookLM recovery and Obsidian archiving

The public `research-review-03-notebooklm-recovery` skill assumes:

- access to NotebookLM
- one stable Obsidian note-writing path
- if live response extraction is needed, a browser automation path

Recommended helpers:

- Obsidian CLI or equivalent
- `web-access` if the recovery source is a live NotebookLM page

## Skills assumed by the workflow

The public versions of the three core skills assume the availability of helper skills or equivalent capabilities for:

- CNKI search
- CNKI detail-page parsing
- CNKI PDF download
- Google Scholar search
- Google Scholar citation chaining
- Google Scholar full-text discovery
- Zotero collection lookup and verification
- Obsidian note writing
- NotebookLM question execution

You may replace the exact helper skills with equivalent tooling in your own environment.

## Minimal install target

If a new user only wants the shortest list needed to make the workflow understandable and runnable, the minimum practical stack is:

- the 3 public workflow skills in this repository
- `cnki-search`
- `cnki-advanced-search`
- `cnki-parse-results`
- `cnki-paper-detail`
- `cnki-download`
- `gs-search`
- `gs-advanced-search`
- `gs-cited-by`
- `gs-fulltext`
- `web-access`
- Zotero MCP or another verified Zotero path
- Obsidian CLI or another verified Obsidian path
- NotebookLM access

Without these helpers, the public workflow files are still readable, but not fully executable end to end.

## Environment-specific notes

### CNKI access

CNKI often depends on:

- institutional access or a valid local login
- a stable browser session
- a correct local proxy or bypass setup

This repository does not ship a universal CNKI connectivity fix. If CNKI is behind a local proxy, adapt the access logic to your own machine and network.

### Zotero

The workflow assumes that a paper is not considered complete unless:

- the item is in the correct collection
- the PDF is attached to that item

Some environments may prefer:

- Zotero MCP
- Zotero local connector
- PyZotero
- Zotero Web API

Use the most stable path in your own environment.

### NotebookLM

NotebookLM execution can be split into:

- prompt design
- source upload
- visible execution
- response recovery

The workflow assumes human review remains part of the loop.

## Suggested repository adaptation

Before using these skills in another environment, replace:

- local absolute paths
- machine-specific download directories
- private vault names
- personal account names
- local helper scripts

with your own configurable paths or environment variables.
