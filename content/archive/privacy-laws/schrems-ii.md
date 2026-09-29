---
title: 'Schrems II (Case C-311/18)'
description: 'The Court of Justice judgment that invalidated the EU-US Privacy Shield and required a case-by-case assessment of transfers to the United States.'
category: 'privacy-laws'
date: '2026-09-27'
eventDate: '2018-07-16'
status: 'adopted'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'In Case C-311/18 the Court of Justice held that the EU-US Privacy Shield was invalid, and that the Standard Contractual Clauses could not alone authorise a transfer where the importer is subject to US law that conflicts with the clauses. Controllers were required to verify the lawfulness of equivalent protection in the destination country.'
claims:
  - type: fact
    text: 'The judgment was delivered on 16 July 2018 in Case C-311/18, Schrems v Data Protection Commissioner.'
  - type: fact
    text: 'The Court held the EU-US Privacy Shield Decision (Commission Implementing Decision (EU) 2016/1707) invalid.'
  - type: fact
    text: 'The Court held that the Standard Contractual Clauses adopted by Commission Implementing Decision (EU) 2021/914 are not sufficient in themselves where the importer is subject to surveillance measures that conflict with them.'
  - type: fact
    text: 'The Court held that the supervisory authority must suspend or prohibit a transfer where equivalent protection cannot be ensured.'
  - type: fact
    text: 'The operative part of the judgment was 96 pages. Paragraph 133 is frequently cited for the assessment of third-country law.'
  - type: source-claim
    text: 'The European Commission and data protection authorities have described the resulting assessment procedure as workable and as a "robust" mechanism. Those are institutional characterisations, not findings in the judgment.'
affected:
  - 'Controllers and exporters in the European Economic Area transferring personal data to the United States'
dataCategories:
  - 'Personal data subject to Chapter V transfers'
geographicScope:
  - 'European Union'
  - 'United States'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['eu', 'x-eea', 'ie']
crossBorder: true
sources:
  - title: 'Judgment of 16 July 2018, Schrems v Data Protection Commissioner, C-311/18'
    url: 'https://curia.europa.eu/juris/liste.jsf?num=C-311/18&language=en'
    publisher: 'Court of Justice of the European Union'
    kind: 'court'
    accessed: '2026-09-27'
  - title: 'Judgment of 6 October 2015, Schrems v Data Protection Commissioner, C-362/14'
    url: 'https://curia.europa.eu/juris/liste.jsf?num=C-362/14&language=en'
    publisher: 'Court of Justice of the European Union'
    kind: 'court'
    note: 'The earlier judgment that struck down Safe Harbor.'
    accessed: '2026-09-27'
  - title: 'Commission Implementing Decision (EU) 2021/914 on standard contractual clauses'
    url: 'https://eur-lex.europa.eu/eli/dec_impl/2021/914/oj'
    publisher: 'Publications Office of the European Union'
    kind: 'regulator'
    accessed: '2026-09-27'
tags: ['data-protection', 'european-union', 'transfers']
related:
  guides: ['encryption/encryption-explained']
  archive: ['privacy-laws/gdpr', 'privacy-laws/eu-digital-services-act']
  news: []
---

## The chain of cases

| Case                              | Date           | Outcome                                     |
| --------------------------------- | -------------- | ------------------------------------------- |
| C-362/14 (Schrems I)              | 6 October 2015 | Safe Harbor invalidated                     |
| Privacy Shield Decision 2016/1707 | 2016           | New adequacy decision for the United States |
| C-311/18 (Schrems II)             | 16 July 2018   | Privacy Shield invalidated                  |

## What the 2018 judgment actually held

The question referred was narrow: whether the Standard Contractual Clauses could continue
to be used for transfers to a third country where the legal system of that country
prevents compliance.

The Court held that they cannot, on their own, and that a transfer requires a verifiable
finding that the importer will in practice respect the clauses. Where the destination
country's law allows authorities to compel access to data and imposes obligations
directly on the importer, the SCCs require the exporter to assess that law and to suspend
the transfer if protection is not ensured.

:::warning
The judgment did not prohibit transfers to the United States, and it did not find that US
law automatically defeats the clauses in every case. It set out a test to be applied case
by case. Statements that it "banned data transfers" or that "the EU banned the US Privacy
Shield, full stop" describe the invalidation of the adequacy decision, not the whole
holding.
:::

## What followed

- The EU-US Privacy Shield framework was replaced by the EU-US Data Privacy Framework
  adequacy decision, which relies on a different legal instrument.
- The 2021 SCCs replaced the earlier ones, with clauses intended to address the issue the
  judgment identified.
- A data protection authority may require an exporter to suspend or prohibit a transfer
  where the assessment does not conclude that protection is ensured.
- The tension between the judgment's reasoning and the later adequacy decision remains
  the subject of pending litigation, which is why this entry's status is not recorded as
  finally settled.

## Limits of this entry

This entry summarises what the judgment held. It does not assess the current state of
litigation, which changes. Check the
[Court of Justice case record](https://curia.europa.eu/juris/liste.jsf?num=C-311/18&language=en)
for the authoritative text and any subsequent references.

## Sources

- [C-311/18, judgment of 16 July 2018](https://curia.europa.eu/juris/liste.jsf?num=C-311/18&language=en)
  — the primary record.
- [C-362/14, judgment of 6 October 2015](https://curia.europa.eu/juris/liste.jsf?num=C-362/14&language=en)
  — Safe Harbor.
- [Commission Implementing Decision (EU) 2021/914](https://eur-lex.europa.eu/eli/dec_impl/2021/914/oj)
  — the current standard contractual clauses.
