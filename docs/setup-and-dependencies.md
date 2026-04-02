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
