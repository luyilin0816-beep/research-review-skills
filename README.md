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
- CNKI-related skills
- Google Scholar-related skills
- Zotero and a usable Zotero connector or Zotero MCP
- Obsidian and an Obsidian CLI workflow
- NotebookLM access
- A browser automation path, such as Chrome MCP or an equivalent web-access layer

See [docs/setup-and-dependencies.md](./docs/setup-and-dependencies.md) for setup notes and environment assumptions.

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
