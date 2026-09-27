---
title: 'Search Engine Privacy'
description: 'Why a search query is one of the most revealing strings you type, and what the alternatives actually change.'
category: 'search-engines'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['search-engines', 'metadata', 'data-broker', 'profiling']
status: 'published'
sources:
  - title: 'Google Privacy Policy'
    url: 'https://policies.google.com/privacy'
    publisher: 'Google LLC'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'DuckDuckGo Privacy Policy'
    url: 'https://duckduckgo.com/privacy'
    publisher: 'DuckDuckGo'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'Brave Search: Independent Index'
    url: 'https://search.brave.com/'
    publisher: 'Brave Software'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'Unique in the Crowd: The privacy bounds of human mobility'
    url: 'https://doi.org/10.1038/srep01359'
    publisher: 'Scientific Reports'
    kind: 'academic'
    note: 'de Montjoye et al., 2013, on re-identification from movement traces.'
    accessed: '2026-09-27'
related:
  guides:
    ['metadata/metadata-explained', 'browsers/choosing-a-browser', 'metadata/metadata-explained']
  archive: []
  news: []
---

A search query is a statement of what you want to know, typed before you have decided who
should know it. Over time, the set of queries is a map of your concerns: your health, your
finances, your relationships, your location, and your job.

## What the record looks like

A major search engine, used with an account, can associate with you:

- each query, with a timestamp
- your IP address and a coarse location derived from it
- the device, browser, and language settings
- links you click in the results, and the sites you then visit

Used without an account, the log is tied to an IP address instead, which in practice still
resolves to a household or an office.

:::warning
"Erase my search history" removes rows from a list you were shown. It does not remove
data already derived from that history, and it does not reach copies in commercial
databases. The
[Unique in the Crowd](https://doi.org/10.1038/srep01359) result is the standard
reference for how little movement data is needed to single out a person.
:::

## What changing engine actually changes

|                        | Personalised results       | Query logging                                                | Model funding              |
| ---------------------- | -------------------------- | ------------------------------------------------------------ | -------------------------- |
| Google with an account | Yes, extensive             | Yes, tied to the account                                     | Advertising                |
| Google signed out      | Limited                    | Yes, tied to IP and cookies                                  | Advertising                |
| DuckDuckGo             | No personal search profile | Claims not to save queries; Bing supplies some results       | Advertising, donations     |
| Brave Search           | No personal profile        | Search activity not stored on the server in the free product | Subscription and licensing |
| SearxNG, self-hosted   | Only what you configure    | Whatever your instance logs — often nothing                  | Yours                      |
| A local index          | No                         | No                                                           | Yours                      |

Two structural differences matter more than the policy comparison. The first is whether
the engine operates its **own index** or resells results from another company's engine,
which changes what the second company learns. The second is **self-hosting**: SearxNG or a
local index means the query never leaves your machine, at the cost of result quality and
your own maintenance.

:::note
Reading a vendor privacy policy tells you what a company says it does, not what it does.
Where a policy is specific and testable — a named retention period, a documented deletion
path, an independent audit — it is worth more than a general assurance. Where it is not,
assume the data is kept and treat the difference accordingly.
:::

## Practical steps

1. Use a browser that does not send a search referrer, or clear it. Most sites log the
   search engine and the query as a `Referer` header.
2. Turn on [Do Not Send My Queries](https://support.google.com/websearch/answer/179386)
   or the equivalent in the search engine you use, if it offers one.
3. Set a search engine that does not require an account.
4. Delete the existing record, and understand that this is partial.
5. Be aware that the _network_ still sees the lookup, unless you use
   [encrypted DNS](/guides/dns/dns-privacy/) or
   [Tor](/guides/tor/what-is-tor/).
6. Remember that a query can identify someone else. Searching for a rare medical symptom or
   a specific address is a disclosure about a person other than you.

## Sources

- [Google Privacy Policy](https://policies.google.com/privacy) — the authoritative
  statement of what is collected, in the company's own words.
- [DuckDuckGo Privacy Policy](https://duckduckgo.com/privacy) — including the
  explanation of what is shared with Microsoft for search results.
- [Brave Search](https://search.brave.com/) — independent index, no stored search history
  in the free tier; a vendor claim, worth testing rather than trusting.
- [de Montjoye et al., _Unique in the Crowd_](https://doi.org/10.1038/srep01359) —
  _Scientific Reports_ 3, 2013.
