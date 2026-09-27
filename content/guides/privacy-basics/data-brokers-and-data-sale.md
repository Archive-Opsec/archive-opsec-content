---
title: 'Data brokers and the market for personal information'
description: 'How personal information is collected, combined, scored and resold, and where practical limits on collection begin.'
category: 'privacy-basics'
updated: '2026-09-27'
added: '2026-09-27'
author: 'Archive-Opsec contributors'
contributors: []
difficulty: 'intermediate'
tags: ['data-broker', 'data-minimisation', 'metadata', 'privacy']
featured: false
status: 'published'
sources:
  - title: 'Data brokers'
    url: 'https://www.ftc.gov/system/files/documents/reports/data-brokers-call-transparency-accountability-report-federal-trade-commission-may-2014/140527databrokerreport.pdf'
    publisher: 'Federal Trade Commission'
    kind: 'regulator'
    accessed: '2026-09-27'
  - title: 'Data and Goliath'
    url: 'https://www.schneier.com/books/data-and-goliath/'
    publisher: 'Bruce Schneier'
    kind: 'academic'
    accessed: '2026-09-27'
related:
  guides: ['metadata/metadata-explained', 'mobile/mobile-device-privacy', 'threat-modeling/define-your-threat-model']
  archive: ['research-papers/unique-in-the-crowd-2013']
  news: []
---

## What a data broker does

A data broker is an organisation whose business model involves collecting, combining, analysing,
licensing or selling information about people. The information may come from public records,
commercial transactions, apps, advertising systems, loyalty programmes, location data or other
brokers. The important point is not the label. It is the chain: one record that looks harmless can
become identifying when it is joined to several others.

The broker may not know your name at first. A device identifier, advertising identifier, hashed
email address, household address, purchase pattern or location trail can still act as a join key.
Pseudonyms reduce direct exposure in some systems, but they do not automatically make the data
anonymous.

## What you can realistically control

You cannot opt out of every public record or make every organisation forget a lawful transaction.
You can reduce the amount of information that is generated and the number of places it is copied:

1. Do not give a real phone number or address to a service that has no reason to need it.
2. Turn off advertising identifiers and unnecessary location access.
3. Avoid signing in to unrelated services with the same identity when separation matters.
4. Delete old accounts and revoke third-party app access.
5. Use access and deletion rights where the applicable law gives you one.

The last step is maintenance, not magic. A deletion request to one company does not remove a copy
held by another company, a public record, or a derived score.

:::warning
Do not use a data-broker opt-out service that asks you to surrender more identity information than
you are comfortable sharing. Verify who receives the request and what evidence is required.
:::

## A useful threat-model question

Ask what decision the data could influence. The risk is not limited to embarrassing disclosure.
Location history, inferred health interests, household composition and financial behaviour can be
used to target, rank, deny, manipulate or surveil people.
