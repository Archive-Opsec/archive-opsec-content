---
title: 'Signal subpoena transparency record'
description: 'Signal published the limited account information it could provide in response to a subpoena.'
category: 'corporate-privacy'
date: '2026-09-27'
eventDate: '2016-03'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'Signal published a transparency record showing that, for the accounts covered by the legal demand, the service could provide only a small amount of account metadata because message content and many other records were not available to it.'
claims:
  - type: source-claim
    text: 'Signal describes what it received and what it could produce in response to the subpoena.'
  - type: fact
    text: 'A transparency record demonstrates the providers data retention design for the specified period, not a guarantee that every future deployment has identical retention.'
affected: ['Signal users covered by the legal demand']
dataCategories: ['Account creation time', 'Last connection time']
geographicScope: ['United States']
# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['us']
crossBorder: false
sources:
  - title: 'Signal and the subpoena'
    url: 'https://signal.org/bigbrother/'
    publisher: 'Signal'
    kind: 'company'
    accessed: '2026-09-27'
tags: ['metadata', 'end-to-end-encryption', 'transparency']
related:
  guides: ['messaging/end-to-end-encrypted-messaging']
  archive: []
  news: []
---

## What is documented

This is a provider transparency record. It is useful for understanding the difference between encrypted message content and the small amount of account metadata a service may retain.
