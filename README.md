# Research Review Skills

A public workflow and skill set for Chinese social science literature review using Codex, CNKI, Google Scholar, Zotero, Obsidian, and NotebookLM.

## What this repository contains

This repository publishes a three-step pre-writing workflow for literature review work:

1. `research-review-01-keyword-calibration-search`
   - calibrate research questions and keywords
   - search CNKI and Google Scholar
   - review candidates with a human in the loop
   - ingest approved papers into Zotero with PDFs
2. `research-review-02-notebooklm-prompts-execution`
   - build module-based review outlines
   - map modules to papers
   - generate NotebookLM-ready prompts
   - support visible, human-audited NotebookLM execution
3. `research-review-03-notebooklm-recovery`
   - recover selected NotebookLM responses
   - preserve raw versions
   - merge or clean them on demand
   - archive them into Obsidian

It also includes a high-level workflow document that explains how the three skills fit together.

## Repository structure

```text
docs/
  workflow-overview.md
  setup-and-dependencies.md
skills/
  research-review-01-keyword-calibration-search/
    SKILL.md
  research-review-02-notebooklm-prompts-execution/
    SKILL.md
  research-review-03-notebooklm-recovery/
    SKILL.md
```

## Design principles

- Human approval remains the default gate at critical steps.
- Candidate lists are not final results.
- A Zotero item is not considered complete unless the PDF is attached.
- NotebookLM is used for module drafting, not for replacing scholarly judgment.
- Intermediate results should be structured, reusable, and auditable.

## Recommended workflow

1. Clarify topic, object, question, and keyword boundaries.
2. Search CNKI and Google Scholar.
3. Stop for human review after the candidate list.
4. Only after approval, fetch PDFs and ingest papers into Zotero.
5. Generate a structured Obsidian summary note.
6. Build module-based review outlines.
7. Upload module PDFs to NotebookLM and execute prompts.
8. Recover approved NotebookLM responses back into Obsidian.

## Dependencies

This repository does not bundle every external tool. A typical working environment includes:

- Codex with local skills enabled
- CNKI helper skills
- Google Scholar helper skills
- Zotero and a usable Zotero connector or Zotero MCP
- Obsidian and an Obsidian CLI workflow
- NotebookLM access
- A browser automation path, such as Chrome MCP or an equivalent web-access layer

### Required helper skills by stage

The three public skills in this repository are not fully standalone. They assume the following helper skills or equivalent capabilities are already available in your Codex environment.

#### Stage 1: `research-review-01-keyword-calibration-search`

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
- a usable Zotero integration path
- an Obsidian note-writing path

#### Stage 2: `research-review-02-notebooklm-prompts-execution`

- a visible browser automation path, such as `web-access` or an equivalent Chrome automation layer
- a usable Zotero integration path for locating source PDFs
- NotebookLM access

#### Stage 3: `research-review-03-notebooklm-recovery`

- Obsidian note-writing capability
- NotebookLM access
- if recovery is done from a live browser session, a browser automation path

### Required MCP or equivalent integrations

In practice, most users will need at least:

- a Zotero MCP or an equivalent local Zotero connector
- an Obsidian CLI or equivalent note-writing automation
- a browser automation layer
- NotebookLM access

See [docs/setup-and-dependencies.md](./docs/setup-and-dependencies.md) for a more explicit dependency checklist.

## Important note on portability

The workflow in this repository was refined on a Windows machine with local browser automation, local Zotero tooling, and a CNKI access workaround. Machine-specific paths, credentials, and private environment details have been removed from this public version.

You should adapt:

- download directories
- proxy or CNKI access settings
- Zotero local integration path
- Obsidian vault path
- NotebookLM login and browser automation strategy

to your own environment.

## License

MIT
