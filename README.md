# Archive-Opsec Content

Public editorial content for [Archive-Opsec](https://archive-opsec.com).

This repository contains the guides, archive records, news digests, resource references, and source records that are published by the private Archive-Opsec website application. It does not contain the website source code, deployment configuration, credentials, or unpublished editorial notes.

## Structure

```text
content/
  guides/
  archive/
  news/
  resources/
data/
  sources/
```

All entries are Markdown files with YAML frontmatter. Archive records should distinguish documented facts, source claims, researcher analysis, and editorial context. Do not republish complete copyrighted articles; include short factual summaries and links to the original sources.

## Editorial rules

- Prefer primary sources: official statements, regulators, courts, standards bodies, academic papers, and government records.
- Include HTTPS source URLs for factual claims.
- Mark uncertain or unverified information honestly.
- Do not commit secrets, private correspondence, personal data, or unpublished investigation notes.
- Do not add placeholder organisations, fabricated events, invented statistics, or synthetic sources.

The private site repository validates this content during its build. See [CONTRIBUTING.md](CONTRIBUTING.md) for the authoring workflow.

## Ways to help

- Submit a pull request with a complete, source-linked entry.
- Open a [content proposal](https://github.com/Archive-Opsec/archive-opsec-content/issues/new?template=content-proposal.yml) for an idea you want reviewed first.
- Report a factual problem using the [correction form](https://github.com/Archive-Opsec/archive-opsec-content/issues/new?template=correction.yml).
