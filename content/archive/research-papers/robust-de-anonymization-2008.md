---
title: 'Robust De-anonymization of Large Sparse Datasets'
description: 'A study showing how auxiliary information can be used to re-identify records in a sparse dataset.'
category: 'research-papers'
date: '2026-09-27'
eventDate: '2008-05-18'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'The paper examined de-anonymisation of sparse, high-dimensional datasets and showed how outside information can link records back to individuals despite removal of direct identifiers.'
claims:
  - type: fact
    text: 'The paper was presented at the 2008 IEEE Symposium on Security and Privacy and is identified by DOI 10.1109/SP.2008.33.'
  - type: researcher-analysis
    text: 'The paper studies a particular class of datasets and attack assumptions; it is not evidence that every anonymisation method fails in the same way.'
affected: ['People represented in sparse behavioural datasets']
dataCategories: ['Ratings', 'Behavioural records', 'Sparse identifiers']
geographicScope: ['Dataset-specific']
# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['x-international']
crossBorder: false
sources:
  - title: 'Robust De-anonymization of Large Sparse Datasets'
    url: 'https://doi.org/10.1109/SP.2008.33'
    publisher: 'IEEE Symposium on Security and Privacy'
    kind: 'academic'
    accessed: '2026-09-27'
tags: ['anonymity', 'de-anonymisation', 'research']
related:
  guides: ['metadata/metadata-explained', 'privacy-basics/what-privacy-means']
  archive: []
  news: []
---

## Why it matters

Anonymisation depends on the surrounding information environment. A dataset that looks anonymous on its own can become identifying when joined with another dataset.
