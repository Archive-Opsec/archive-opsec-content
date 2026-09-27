---
title: 'Browser Fingerprinting'
description: 'How a device gets identified from the shape of its requests, what resists it, and what a fingerprint is worth.'
category: 'browsers'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['fingerprinting', 'browser', 'browsers', 'tracking']
featured: true
status: 'published'
sources:
  - title: 'Cover Your Tracks'
    url: 'https://coveryourtracks.eff.org/'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    accessed: '2026-09-27'
  - title: 'Browser Fingerprinting: A Survey'
    url: 'https://doi.org/10.1145/3386040'
    publisher: 'ACM Transactions on the Web'
    kind: 'academic'
    note: 'Laperdrix, Bielova, Baudry and Avoine, ACM Transactions on the Web 14(2), article 8, 2020.'
    accessed: '2026-09-27'
  - title: 'resistFingerprinting'
    url: 'https://wiki.mozilla.org/Security/Fingerprinting'
    publisher: 'Mozilla'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'Privacy Principles'
    url: 'https://www.w3.org/TR/privacy-principles/'
    publisher: 'W3C'
    kind: 'standards'
    accessed: '2026-09-27'
related:
  guides: ['browsers/choosing-a-browser', 'search-engines/search-engine-privacy', 'tor/what-is-tor']
  archive: []
  news: []
---

Cookies are easy to delete and easy to block. Fingerprinting was built for the case where
they are not.

## How it works

A script on a page can read a long list of mostly stable properties of your browser and
machine, and combine them into a short string. The inputs include:

- screen dimensions, colour depth, and available fonts
- installed browser plugins and their versions
- time zone, system language, and locale formatting
- graphics rendering details, exposed through the canvas and WebGL APIs
- hardware concurrency, device memory, and battery status
- touch capability and the maximum number of touch points

Each is individually unremarkable. Concatenated, they produce a value that is stable
enough to recognise a returning device.

:::note
The result is not a name. It is a pseudonymous identifier that becomes personally
identifying the moment it appears alongside an account, a login, or a payment. That
transition is why fingerprinting is regulated: the identifier becomes data about a person
without the person ever being named.
:::

## Why blocking is hard

- **It needs no storage.** Nothing is written to your device, so clearing cookies and site
  data does nothing.
- **It is a script, not a request.** A content blocker can stop known third-party requests.
  Fingerprinting code frequently runs from the first-party origin, where blocking it
  breaks the site.
- **It is a strong signal in aggregate.** A site does not need a _stable_ fingerprint.
  Combining many weak signals over many visits identifies a device reliably, which is why
  changes are deliberately made slowly.

## What resists it

**Uniformity across the population.** The strongest defence is being unremarkable: a
browser configuration that matches the most common one. This is the approach Firefox
implements in `privacy.resistFingerprinting`, which pins the reported values to a standard
set and refuses site-specific overrides. The cost is a small number of sites that
misbehave.

**Isolation.** Reducing the number of distinct identifiers, partitioning storage, and
resisting linkable cross-site identifiers all break the aggregation step.

**The strongest option: Tor Browser.** It fixes the values to what a mainstream browser
looks like _and_ gives every user the same values, so there is no long tail to single
out. It is the only approach that makes a device genuinely unremarkable rather than
merely unusual. See [what Tor is](/guides/tor/what-is-tor/).

:::warning
"Rounded corners", "blur on the UI" and other visual customisations are cosmetic and do
nothing for fingerprinting. Extensions that claim to defeat fingerprinting without
standardising configuration generally add unique surface area instead of removing it.
:::

## Measuring it

[Cover Your Tracks](https://coveryourtracks.eff.org/) runs a standard test in your
browser and reports how many of the known fingerprinting tests your configuration
survives. It is a snapshot of a test suite, not a proof of anything, but it is a useful
comparison between configurations.

## Sources

- [Cover Your Tracks](https://coveryourtracks.eff.org/) — EFF's ongoing survey of
  fingerprinting defences in real browsers.
- [Browser Fingerprinting: A Survey](https://doi.org/10.1145/3386040) — Laperdrix,
  Bielova, Baudry and Avoine, _ACM Transactions on the Web_ 14(2), article 8, 2020. The
  survey reference for what the technique is and how it has been measured.
- [Mozilla wiki: Fingerprinting](https://wiki.mozilla.org/Security/Fingerprinting) — how
  the `resistFingerprinting` preference is implemented and what it costs.
- [W3C Privacy Principles](https://www.w3.org/TR/privacy-principles/) — the current
  standards work on reducing identifying information in web requests.
