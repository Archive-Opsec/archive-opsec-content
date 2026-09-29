---
title: 'Apple App Tracking Transparency'
description: 'Apple introduced a permission requirement for app tracking across companies and access to the advertising identifier.'
category: 'corporate-privacy'
date: '2026-09-27'
eventDate: '2021-04'
status: 'adopted'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'Apple introduced App Tracking Transparency as a framework requiring apps to request permission before tracking a user across apps and websites owned by other companies.'
claims:
  - type: fact
    text: 'Apple documents App Tracking Transparency as the framework for requesting permission to track a user or access the advertising identifier.'
  - type: source-claim
    text: 'Apples documentation describes the intended privacy effect; it does not establish that all forms of measurement or first-party analytics are blocked.'
affected: ['Users of apps distributed through Apple platforms', 'App developers and advertisers']
dataCategories: ['Advertising identifier', 'Cross-app activity signals']
geographicScope: ['Apple platform users globally']
# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['x-tech', 'us']
crossBorder: true
sources:
  - title: 'AppTrackingTransparency framework documentation'
    url: 'https://developer.apple.com/documentation/apptrackingtransparency'
    publisher: 'Apple Developer'
    kind: 'documentation'
    accessed: '2026-09-27'
tags: ['tracking', 'advertising', 'data-minimisation']
related:
  guides: ['mobile/mobile-device-privacy']
  archive: []
  news: []
---

## What is documented

The framework changes the permission model for cross-company tracking on Apple platforms. It does not make an app anonymous, and it does not remove all first-party collection.
