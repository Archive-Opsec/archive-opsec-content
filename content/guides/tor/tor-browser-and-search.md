---
title: 'Tor Browser and Searching on Tor'
description: 'The configuration that makes Tor usable, why the fingerprint is identical for everyone, and how onion search works.'
category: 'tor'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['tor', 'fingerprinting', 'search-engines', 'onion-routing']
status: 'published'
sources:
  - title: 'Download Tor Browser'
    url: 'https://www.torproject.org/download/'
    publisher: 'The Tor Project'
    kind: 'ngo'
    note: 'The former /browser/ page was removed in the Tor Project site reorganisation. This download page is the current canonical location and resolves to download.torproject.org.'
    accessed: '2026-09-27'
  - title: 'Tor Browser Manual'
    url: 'https://tb-manual.torproject.org/'
    publisher: 'The Tor Project'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'SearxNG'
    url: 'https://docs.searxng.org/'
    publisher: 'SearxNG contributors'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides:
    ['tor/what-is-tor', 'browsers/browser-fingerprinting', 'search-engines/search-engine-privacy']
  archive: []
  news: []
---

Tor Browser is Firefox configured so that every user's browser is indistinguishable from
every other user's browser. That single design decision is what makes it a privacy tool
rather than a routing tool.

## Why the configuration is the point

[Browser fingerprinting](/guides/browsers/browser-fingerprinting/) works by finding values
that make you unusual. Tor Browser removes unusualness by fixing the values:

- window size, screen dimensions, timezone, and locale are standardised
- WebRTC and other APIs that leak local network information are disabled
- canvas and font lists are quantised so that minor system differences disappear
- every user looks the same to every site, so there is no long tail to single out
- the browser refuses to let a site override these settings

:::note
This is why "Tor Browser with extensions" or "Tor with a custom theme" is a
contradiction. An extension that changes any fingerprinted value, or a preference that
differs from the shipped default, makes you distinguishable. Upstream builds are
designed so that using them exactly as shipped is the privacy-preserving act.
:::

## Practical configuration

- Take Tor Browser from [torproject.org](https://www.torproject.org/download/) or a
  reputable mirror, and verify the signature if the distribution channel allows it.
- Do not install extensions. Do not change the window size.
- Leave the default bridge, security level, and fingerprint settings alone unless there
  is a reason.
- Use a separate profile for work versus personal browsing only if you understand that
  separate profiles on one machine are not separate people; the fingerprint is the same
  either way.

## Onion search

Searching the normal web through Tor sends the query over the circuit, so the search
engine sees an exit relay. Search engines also treat Tor traffic as a bot signal, so
results are frequently degraded or blocked.

An **onion service search engine** removes both problems: the query never leaves the
network, and there is no bot-detection layer. SearxNG can be run as an onion service, and
several public instances exist. Treat public instances with care: the operator can see
your queries unless the instance is configured to log nothing, and a self-hosted instance
is the only version where that is under your control. See
[SearxNG documentation](https://docs.searxng.org/).

:::warning
A general onion service still depends on what it serves. Searching through it protects the
query from your network and your exit; it does not make the destination or the operator
honest.
:::

## Onions, and sites that block Tor

Some services — banks, most search engines, and a number of content sites — block exit
relay addresses outright. This is a property of those services, not a failure of Tor, and
it cannot be worked around without abandoning the reason for using it.

If the site blocks you:

- do not install a bridge to bypass a specific block in a way that defeats your own
  anonymity guarantees
- do not log in to an account from a circuit you care about
- accept that some parts of the web are not reachable this way

## Which mode to use

| Need                                                     | Mode                                     |
| -------------------------------------------------------- | ---------------------------------------- |
| Anonymity from a website, an ad network, a local network | Standard                                 |
| Accessing a site that blocks Tor                         | A bridge, accepting a small setup cost   |
| Reaching a specific onion service directly               | Onion mode, which skips the exit         |
| Maximum resistance in a hostile country                  | The highest security level, and a bridge |

## Sources

- [Download Tor Browser](https://www.torproject.org/download/) — what the project states the
  browser is for, and the download.
- [Tor Browser Manual](https://tb-manual.torproject.org/) — the authoritative reference
  for settings, including the security levels and what each disables.
- [SearxNG documentation](https://docs.searxng.org/) — self-hosting, logging
  configuration, and onion service deployment.
