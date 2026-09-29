---
title: 'General Data Protection Regulation (EU) 2016/679'
description: 'The EU data protection regulation, its scope, and the obligations it created for organisations that process personal data.'
category: 'privacy-laws'
date: '2026-09-27'
eventDate: '2018-05-25'
status: 'adopted'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'Regulation (EU) 2016/679 replaced the 1995 Data Protection Directive. It applies across the EU, raised the maximum fine to a percentage of global annual turnover, and introduced the right to erasure and the concept of data protection by design.'
claims:
  - type: fact
    text: 'The Regulation was adopted on 27 April 2016 and became applicable from 25 May 2018.'
  - type: fact
    text: 'Article 5 sets out the principles of processing, including lawfulness, fairness, transparency, purpose limitation, data minimisation, accuracy, storage limitation, integrity and confidentiality, and accountability.'
  - type: fact
    text: 'Article 4(1) defines personal data as any information relating to an identified or identifiable natural person.'
  - type: fact
    text: 'Article 17 establishes the right to erasure, commonly called the right to be forgotten, in enumerated circumstances.'
  - type: fact
    text: 'Article 83 sets administrative fines up to EUR 20 million, or 4% of total worldwide annual turnover, whichever is higher, for the categories of infringement listed in the Article.'
  - type: fact
    text: 'Article 25 requires data protection by design and by default for the processing of personal data.'
  - type: source-claim
    text: 'The European Commission has described the Regulation as making the EU the hardest jurisdiction in the world for data protection compliance. That is a characterisation by the regulator, not an independent finding.'
affected:
  - 'Controllers and processors established in the EU'
  - 'Controllers and processors outside the EU where processing relates to people in the EU'
dataCategories:
  - 'Personal data as defined in Article 4(1)'
geographicScope:
  - 'European Union'
  - 'EEA, via the EEA Agreement'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['eu', 'x-eea']
crossBorder: true
sources:
  - title: 'Regulation (EU) 2016/679 (General Data Protection Regulation)'
    url: 'https://eur-lex.europa.eu/eli/reg/2016/679/oj'
    publisher: 'Publications Office of the European Union'
    kind: 'regulator'
    accessed: '2026-09-27'
  - title: 'GDPR text on EUR-Lex, all consolidated versions'
    url: 'https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679'
    publisher: 'Publications Office of the European Union'
    kind: 'regulator'
    accessed: '2026-09-27'
  - title: 'Schrems II (C-311/18) and the transfer mechanism in question'
    url: 'https://curia.europa.eu/juris/liste.jsf?num=C-311/18&language=en'
    publisher: 'Court of Justice of the European Union'
    kind: 'court'
    accessed: '2026-09-27'
tags: ['data-protection', 'european-union', 'right-to-be-forgotten']
related:
  guides: ['privacy-basics/what-privacy-means']
  archive: ['privacy-laws/schrems-ii', 'privacy-laws/eu-digital-services-act']
  news: []
---

## What the Regulation is

The GDPR is the binding text. It replaced Directive 95/46/EC, which set a floor that
member states implemented with a great deal of variation, and it removed most of that
variation by making the rules directly applicable.

## Why it mattered

Three things changed in ways that were visible outside Europe:

1. **Territorial reach.** Article 3 extends the Regulation to processing outside the EU
   where the processing relates to people in the EU. This is why a non-EU organisation
   with EU users had to read it.
2. **The fine scale.** Administrative fines are expressed partly as a percentage of
   worldwide turnover, so enforcement is no longer limited by the size of a local
   operation.
3. **Enforceable individual rights.** Access, rectification, erasure, portability, and
   objection are rights a person can exercise, not principles an organisation may
   consider.

## What it did not do

The GDPR is a data protection instrument, not a secrecy instrument. It regulates the
processing of personal data by identifiable controllers; it does not in general prohibit
collection, and it says nothing about traffic analysis or metadata that does not relate
to an identified person. It also has no extraterritorial application to
non-personal-data surveillance, and enforcement remains national through
data protection authorities.

:::note
A widely repeated claim is that the GDPR "bans" surveillance. The Regulation does not. It
constrains the processing of personal data, and a mass-surveillance programme that does
not process personal data, or that is itself lawful under a separate instrument, is
outside its reach.
:::

## The parts that get cited most

| Provision          | Subject                                                                |
| ------------------ | ---------------------------------------------------------------------- |
| Article 4          | Definitions, including personal data, processing, and pseudonymisation |
| Article 5          | Principles of processing                                               |
| Article 6          | Lawful bases for processing                                            |
| Article 13, 14     | Information to be provided to data subjects                            |
| Article 17         | Right to erasure                                                       |
| Article 20         | Data portability                                                       |
| Article 25         | Data protection by design and by default                               |
| Article 33, 34     | Breach notification to the authority and to data subjects              |
| Article 35         | Data protection impact assessment                                      |
| Article 44 onwards | International transfers                                                |
| Article 83         | Administrative fines                                                   |

## Transfers

Article 44 established that personal data may leave the European Economic Area only under
one of the mechanisms in Chapter V. Adequacy decisions, appropriate safeguards such as
standard contractual clauses, and derogations are the three routes. The adequacy decisions
have been litigated repeatedly, which is why
[Schrems II](/archive/privacy-laws/schrems-ii/) is tracked separately.

## Sources

- [Regulation (EU) 2016/679 on EUR-Lex](https://eur-lex.europa.eu/eli/reg/2016/679/oj) — the authoritative text. Article numbers cited above refer to this text.
- [CELEX 32016R0679](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32016R0679)
  — the same instrument with its consolidated versions, useful for amendments and
  corrigenda.
- [CJEU case list for C-311/18](https://curia.europa.eu/juris/liste.jsf?num=C-311/18&language=en)
  — the judgment that reshaped the transfer regime.
