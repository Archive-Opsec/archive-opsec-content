---
title: 'Choosing a Browser'
description: 'What the three main engines do differently for privacy, and a decision order that fits most people.'
category: 'browsers'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['browser', 'browsers', 'open-source', 'fingerprinting']
status: 'published'
sources:
  - title: 'Firefox Privacy'
    url: 'https://www.mozilla.org/firefox/privacy/'
    publisher: 'Mozilla Foundation'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'Tor Browser'
    url: 'https://www.torproject.org/download/'
    publisher: 'The Tor Project'
    kind: 'ngo'
    accessed: '2026-09-27'
  - title: 'Brave Privacy'
    url: 'https://brave.com/privacy/'
    publisher: 'Brave Software'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'Browser Fingerprinting: A Survey'
    url: 'https://doi.org/10.1145/3386040'
    publisher: 'ACM Transactions on the Web'
    kind: 'academic'
    note: 'Laperdrix, Bielova, Baudry and Avoine, ACM Transactions on the Web 14(2), article 8, 2020.'
    accessed: '2026-09-27'
related:
  guides:
    ['browsers/browser-fingerprinting', 'search-engines/search-engine-privacy', 'tor/what-is-tor']
  archive: []
  news: []
---

Almost all browsing happens in a browser that runs code you did not write, on a page
controlled by someone else, over a connection you cannot see. The browser is therefore the
highest-leverage place to make privacy decisions.

## The realistic shortlist

**Firefox.** Open source, from a non-profit foundation, and the only mainstream browser
with a built-in preference (`privacy.resistFingerprinting`) that standardises the
properties a fingerprint is built from. It also has strong cookie isolation and
`dFPMR` for total cookie protection. The trade-off: this configuration breaks some sites,
and Firefox's market share is small enough that it is not the default configuration many
sites test against.

**Brave.** Built on Chromium, ships third-party cookie blocking and fingerprint
resistance by default, and funds its own search index so it does not depend on
search-ad revenue in the way that constrains Chrome. The trade-off: it is not
open source in the usual sense, and its own additions are trust decisions you are making.

**Tor Browser.** Firefox with a much stronger configuration: every user gets identical
values, so users are indistinguishable from each other. The trade-off is throughput and
that some sites block it. If your model includes not wanting to be identifiable at all,
this is the only good answer.

:::note
Chromium itself is not the privacy problem; the default configuration of Google Chrome
is. A Chromium-based browser with aggressive blocking and fingerprint resistance will
outperform a stock Chrome installation on every dimension that matters. There is no
reason a privacy choice has to be a monoculture.
:::

## A decision order

1. **Do I need to be unidentifiable?** If yes, use Tor Browser and accept the slowness.
   Nothing else gets you there.
2. **Do I need to browse normally, with far less fingerprinting?** Use Firefox with
   `privacy.resistFingerprinting` enabled, or a hardened Chromium build.
3. **Do I mainly want tracking blocked?** Any of the above, with content blocking turned
   on.
4. **Is my main concern corporate data collection rather than tracking?** A browser
   choice barely helps. See [search engine privacy](/guides/search-engines/search-engine-privacy/).

## Turning things on

In Firefox, in about:config:

```text
// Standardise fingerprintable properties
privacy.resistFingerprinting            = true
// Reject trackers in strict mode and isolate state
privacy.trackingprotection.enabled      = true
privacy.trackingprotection.pbmode.enabled = true
// Ask sites not to fingerprint, and treat refusals as breakage
privacy.donottrackheader.enabled        = true
```

:::warning
`privacy.donottrackheader` sends `DNT: 1`. It is a request, not a control, and a small
minority of sites honour it. It is worth enabling as a free signal, but never as a
protection. Fingerprint resistance and third-party blocking are what do the work.
:::

## Extensions worth having

Keep the list short. Each extension is code with your browsing history in scope, so a
small trusted set beats a large one.

- **uBlock Origin** — content blocking, with the annoyance of periodic breakage when
  sites change their scripts. It is the single highest-value extension for reducing
  passive collection.
- **A password manager extension** — see
  [using a password manager](/guides/password-managers/using-a-password-manager/).
- **Nothing else, unless you have a specific reason.** Extension sync is a channel too;
  check what yours sends.

## Sources

- [Firefox privacy features](https://www.mozilla.org/firefox/privacy/) — Mozilla's own
  description of what it enables and when.
- [Tor Browser download and design notes](https://www.torproject.org/download/) — the
  strongest anti-fingerprinting configuration available in a browser.
- [Brave privacy](https://brave.com/privacy/) — described by the vendor; treat the
  self-hosted search claim as a source claim until you have checked it.
