---
title: 'Personal Information Protection Act (Republic of Korea)'
description: 'South Korea’s PIPA, the rights it created, and the enforcement record of the Personal Information Protection Commission.'
category: 'privacy-laws'
date: '2026-09-29'
eventDate: '2011-09-28'
status: 'adopted'
verification: 'unchecked'
lastVerified: '2026-09-29'
summary: 'The Personal Information Protection Act is South Korea’s principal data protection statute. It requires consent for collecting personal information, gives the individual rights of access, correction and deletion, and is enforced by the Personal Information Protection Commission, which can impose administrative fines.'
claims:
  - type: fact
    text: 'The Act was enacted on 29 September 2011 and entered into force on 28 September 2012.'
  - type: fact
    text: 'Article 15 provides that a personal information controller must obtain the consent of the data subject to collect personal information, subject to the exceptions in Articles 17 to 22.'
  - type: fact
    text: 'Articles 18, 19 and 20 establish the rights of a data subject to request access to, correction of, and deletion of their personal information.'
  - type: fact
    text: 'Article 23 sets conditions on provision of personal information to a third party, including the separate written consent requirement in Article 23(2) and its enumerated exceptions.'
  - type: fact
    text: 'Enforcement is carried out by the Personal Information Protection Commission, and the Commission may issue corrective orders and impose administrative fines of up to 100 million KRW for a corporation.'
  - type: source-claim
    text: 'The Commission has been characterised internationally as one of the more assertive data protection regulators. That is an external characterisation, not a finding recorded in the statute.'
affected:
  - 'Personal information controllers and processors in the Republic of Korea'
  - 'Individuals whose personal information is processed in the Republic of Korea'
dataCategories:
  - 'Personal information as defined in Article 2(1)'
geographicScope:
  - 'Republic of Korea'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['kr']
crossBorder: false
sources:
  - title: 'Personal Information Protection Act (English translation)'
    url: 'https://elaw.klri.re.kr/eng_service/lawView.do?hseq=60198&lang=ENG'
    publisher: 'Korea Legislation Research Institute'
    kind: 'government'
    accessed: '2026-09-29'
  - title: 'Personal Information Protection Commission (PIPC)'
    url: 'https://www.pipc.go.kr/eng/'
    publisher: 'Personal Information Protection Commission'
    kind: 'regulator'
    accessed: '2026-09-29'
  - title: 'Act on the Protection of Personal Information Held by Public Institutions'
    url: 'https://elaw.klri.re.kr/eng_service/lawView.do?hseq=63604&lang=ENG'
    publisher: 'Korea Legislation Research Institute'
    kind: 'government'
    accessed: '2026-09-29'
tags: ['data-protection', 'right-to-be-forgotten']
related:
  guides: ['privacy-basics/what-privacy-means']
  archive: ['privacy-laws/gdpr', 'privacy-laws/state-privacy-laws-united-states']
  news: []
---

## What the Act is

PIPA is the general data protection statute for the Republic of Korea. It is
consent-first: unlike a regime built on an enumerated set of lawful bases, the
default rule in Article 15 is that collecting personal information requires the
data subject’s consent, and everything else in the Act is a list of exceptions
to that default.

That default is the single most important structural fact about the statute, and
it is also why PIPA and the GDPR are not interchangeable for a compliance
assessment. A transfer-impact or lawful-basis analysis written for Article 6 of
the GDPR has to be redone from the ground up for PIPA.

## Rights

| Provision  | Subject                                                     |
| ---------- | ----------------------------------------------------------- |
| Article 15 | Consent as the default rule for collection                  |
| Article 18 | Right of access by the data subject                          |
| Article 19 | Right to request rectification                              |
| Article 20 | Right to request deletion                                    |
| Article 23 | Provision of personal information to a third party          |
| Article 24 | Rules on the use of personal information beyond the purpose  |

## Enforcement

The Personal Information Protection Commission is the regulator. It can issue
corrective orders and impose administrative fines, which are the mechanism that
makes a right enforceable rather than decorative. A reader assessing how a
regime actually operates should read the Commission’s own published
enforcement record rather than take the existence of a fine from the statute
table as evidence of its use.

:::note
A separate statute, the Act on the Protection of Personal Information Held by
Public Institutions, applies to public bodies. The two regimes overlap on
biometrics and on large-scale processing, and which one governs is a question
about the controller and the data, not just about the sector.
:::

## What it does not do

PIPA regulates the processing of personal information by identifiable
controllers. It is not a secrecy instrument, it does not in general prohibit
collection, and it says nothing about traffic analysis or metadata that does not
relate to an identified person. A surveillance programme run by a state body is a
question under the public-institutions statute and the relevant national
security legislation, not under PIPA alone.

## Sources

- [Personal Information Protection Act](https://elaw.klri.re.kr/eng_service/lawView.do?hseq=60198&lang=ENG)
  — the statutory text. Article numbers above refer to this translation.
- [Personal Information Protection Commission](https://www.pipc.go.kr/eng/) — the
  regulator, and the place to check current enforcement activity.
- [Act on Personal Information Held by Public Institutions](https://elaw.klri.re.kr/eng_service/lawView.do?hseq=63604&lang=ENG)
  — the parallel regime for public bodies.
