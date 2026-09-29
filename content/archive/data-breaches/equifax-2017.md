---
title: 'Equifax 2017 data breach'
description: 'A 2017 intrusion into Equifax systems exposed personal information held by the credit reporting company.'
category: 'data-breaches'
date: '2026-09-27'
eventDate: '2017-09'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'Equifax disclosed that attackers had accessed systems containing personal information. Regulatory and court records later documented security failures and the resulting consumer settlement.'
claims:
  - type: fact
    text: 'The Federal Trade Commission brought enforcement action relating to the 2017 Equifax breach and consumer remediation.'
  - type: source-claim
    text: 'The affected data categories and population figures in public records are claims made by Equifax or regulators and should be read with the cited records.'
affected: ['Equifax customers and applicants']
dataCategories: ['Names', 'Contact information', 'Government identifiers', 'Credit information']
geographicScope: ['United States']
# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['us']
crossBorder: false
sources:
  - title: 'Equifax data breach settlement and consumer information'
    url: 'https://www.ftc.gov/enforcement/refunds/equifax-data-breach-settlement'
    publisher: 'Federal Trade Commission'
    kind: 'regulator'
    accessed: '2026-09-27'
tags: ['breach', 'data-protection', 'united-states']
related:
  guides: ['privacy-basics/what-privacy-means', 'threat-modeling/common-threats']
  archive: []
  news: []
---

## What is documented

The breach is documented through Equifax disclosures and subsequent regulatory proceedings. This entry records the public record without reproducing settlement or news copy.

## Why it matters

Credit-reporting data is valuable because it combines identity attributes with records used to make decisions about people. A breach of that kind cannot be treated like a password reset alone.
