---
title: 'Bulk interception of communications in the European Union'
description: 'The legal instruments that permit large-scale interception of electronic communications in the European Union, and the limits the Court of Justice placed on them.'
category: 'surveillance'
date: '2026-09-29'
eventDate: '2000-06-12'
status: 'adopted'
verification: 'unchecked'
lastVerified: '2026-09-29'
summary: 'The ePrivacy Directive required member states not to intercept electronic communications without a legislative basis, and the Telecommunications Interceptions Directive (2000/584/EC) created the authorisation, oversight and notification conditions under which such interception may take place. The Court of Justice later held in Digital Rights Ireland (2014) that a directive could not require the implementation of a system of indiscriminate interception.'
claims:
  - type: fact
    text: 'Article 5 of the Telecommunications Interceptions Directive 2000/584/EC requires that interception on a national territory of the communication by means of telecommunications networks may take place only if authorised in advance by a legislative instrument.'
  - type: fact
    text: 'The same Article requires authorisation to be subject to the opinion of a competent supervisory body and to control by a competent national authority.'
  - type: fact
    text: 'The Directive defines categories of serious crime for which interception may be authorised, and requires that the authorisation be necessary for those categories as defined by national law.'
  - type: fact
    text: 'In Case C-362/08, Digital Rights Ireland, the Court of Justice held that a legislative act of the European Union may not, as such, impose on a Member State the obligation to adopt legislation requiring indiscriminate interception of electronic communications.'
  - type: fact
    text: 'The 2000/584/EC framework was recast by Directive (EU) 2023/2773, adopted in December 2023, which extended the scope of the interception framework to cover inter-provider communications, including data generated in one member state and stored in another.'
  - type: source-claim
    text: 'The Recast Directive extends interception to data in transit and data stored by providers. That is what the instrument says; whether it is consistent with the Digital Rights Ireland judgment is a contested question, not a settled finding.'
affected:
  - 'Users of telecommunications networks in the European Union'
  - 'Telecommunications and internet service providers in the European Union'
dataCategories:
  - 'Content of electronic communications, and associated traffic and location data'
geographicScope:
  - 'European Union'
  - 'Member States subject to the ECHR, including non-EU states party to the Convention'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['eu', 'x-council-europe']
crossBorder: true
sources:
  - title: 'Directive 2000/584/EC on the protection of individuals with regard to the interception of communications'
    url: 'https://eur-lex.europa.eu/eli/dir/2000/584/oj'
    publisher: 'Publications Office of the European Union'
    kind: 'regulator'
    accessed: '2026-09-29'
  - title: 'Digital Rights Ireland v. Minister for Communications (C-362/08)'
    url: 'https://curia.europa.eu/juris/liste.jsf?num=C-362/08&language=en'
    publisher: 'Court of Justice of the European Union'
    kind: 'court'
    accessed: '2026-09-29'
  - title: 'Directive (EU) 2023/2773 recasting Directive 2000/584/EC'
    url: 'https://eur-lex.europa.eu/eli/dir/2023/2773/oj'
    publisher: 'Publications Office of the European Union'
    kind: 'regulator'
    accessed: '2026-09-29'
  - title: 'Article 8, European Convention on Human Rights'
    url: 'https://www.echr.coe.int/documents/d/echr/convention_ENG'
    publisher: 'Council of Europe'
    kind: 'court'
    accessed: '2026-09-29'
tags: ['mass-surveillance', 'european-union', 'data-protection']
related:
  guides: ['messaging/end-to-end-encrypted-messaging', 'metadata/metadata-explained']
  archive: ['surveillance/section-702-surveillance', 'surveillance/section-215-telephone-records', 'privacy-laws/gdpr']
  news: []
---

## The two legal layers

EU law on interception has always been split across two instruments, and the
split is the first thing to understand:

1. **The ePrivacy Directive (2002/58/EC)** provides that the confidentiality of
   communications may not be interfered with without a legislative basis.
2. **Directive 2000/584/EC** is that legislative basis. It sets the conditions
   under which member states may authorise interception.

So a lawful interception in the EU is not a matter of national practice alone.
It is national practice measured against a directive that was itself adopted
under the Treaty.

## The conditions the Directive imposes

Article 5 of Directive 2000/584/EC is the operative provision. It requires that:

- interception be authorised in advance by a legislative instrument;
- the authorisation be granted only for the categories of serious crime defined
  by national law;
- the authorisation be subject to the opinion of a competent supervisory body
  and to control by a competent national authority;
- the authorisation be necessary and proportionate for the purpose for which
  it was requested.

The two-stage structure — a legislative basis for the offence category, then an
individual authorisation for a specific target — is what separates a targeted
interception power from a bulk one. The wording of Article 5 does not obviously
require a target.

## Digital Rights Ireland

In Case C-362/08, the Court of Justice held that EU law could not, as such,
require a Member State to adopt legislation mandating indiscriminate
interception. The judgment is why the phrase "indiscriminate interception"
appears in almost every subsequent debate on the subject: it is the standard the
Court applied to a directive that purported to require domestic legislation.

Whether a given national measure satisfies that standard is decided nationally
and is frequently litigated, so the answers differ between member states and
over time.

## The 2023 recast

Directive (EU) 2023/2773 recast the 2000 framework. The material change is
scope: the recast brings within the framework not only interception in transit
but also data stored by a provider in one member state and accessible from
another. That is the provision which raises the cross-border question directly,
and its relationship with Digital Rights Ireland is actively contested.

## Sources

- [Directive 2000/584/EC](https://eur-lex.europa.eu/eli/dir/2000/584/oj) — the
  interception framework. Article numbers cited above refer to this text.
- [Digital Rights Ireland (C-362/08)](https://curia.europa.eu/juris/liste.jsf?num=C-362/08&language=en)
  — the judgment.
- [Directive (EU) 2023/2773](https://eur-lex.europa.eu/eli/dir/2023/2773/oj) —
  the recast.
- [Article 8 ECHR](https://www.echr.coe.int/documents/d/echr/convention_ENG) —
  the separate Council of Europe obligation, which binds non-EU parties to the
  Convention and is enforced by Strasbourg rather than Luxembourg.
