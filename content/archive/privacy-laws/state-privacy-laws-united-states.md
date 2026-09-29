---
title: 'US State Privacy Laws'
description: 'The wave of US state comprehensive privacy statutes from 2020, and what differs between them.'
category: 'privacy-laws'
date: '2026-09-27'
eventDate: '2020-11-03'
status: 'adopted'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'A set of US states enacted comprehensive consumer privacy statutes beginning with the CCPA in 2018, with ballot initiatives and legislative enactments from 2020 onward. The laws differ in thresholds, definitions, whether they create a private right of action, and how they treat sensitive data, children, and sale rather than sharing.'
claims:
  - type: fact
    text: 'The California Consumer Privacy Act was enacted in 2018 and amended by the California Privacy Rights Act in 2020, which took effect on 1 January 2023.'
  - type: fact
    text: 'Virginia enacted the Virginia CDPA in 2020, the first state law to take effect after the CCPA amendment, on 1 January 2023.'
  - type: fact
    text: 'Colorado enacted the Colorado Privacy Act in 2021, effective 1 July 2023.'
  - type: fact
    text: 'Connecticut enacted the Connecticut Data Privacy Act in 2022, effective 1 July 2023.'
  - type: fact
    text: 'Utah enacted the Utah Consumer Privacy Act in 2023, effective 31 December 2023.'
  - type: fact
    text: 'Oregon enacted the Oregon Consumer Privacy Act in 2023, effective 1 July 2024.'
  - type: fact
    text: 'Texas, Florida, and several other states have enacted statutes of varying scope. This entry tracks the legislative acts and does not attempt to summarise the current status of litigation or of every amendment.'
  - type: source-claim
    text: 'Industry bodies and civil liberties organisations have characterised the state laws variously as a patchwork and as a national floor. Both are arguments about policy, not statements of the law.'
affected:
  - 'Controllers meeting each state?셲 statutory threshold'
dataCategories:
  - 'Personal data as each statute defines it'
geographicScope:
  - 'Colorado, Connecticut, Florida, Oregon, Texas, Utah, Virginia, and other US states'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['us']
crossBorder: false
sources:
  - title: 'Virginia CDPA — Code of Virginia, Title 59.1-5200 et seq.'
    url: 'https://law.lis.virginia.gov/vacode/title59.1/chapter52/'
    publisher: 'Virginia Law Library'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'Colorado Privacy Act — CRS Title 6, Part 1'
    url: 'https://leg.colorado.gov/bills/sb21-190'
    publisher: 'Colorado General Assembly'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'Connecticut Data Privacy Act — Connecticut General Statutes'
    url: 'https://www.cga.ct.gov/current/pub/chap_743jj.htm'
    publisher: 'Connecticut General Assembly'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'Utah Consumer Privacy Act — Utah Code Title 13-61'
    url: 'https://le.utah.gov/xcode/Title13/Chapter61/13-61.html'
    publisher: 'Utah State Legislature'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'Oregon Consumer Privacy Act — Oregon Revised Statutes Chapter 646A'
    url: 'https://www.oregonlegislature.gov/bills_laws/ors/ors646A.html'
    publisher: 'Oregon Legislative Assembly'
    kind: 'government'
    note: 'The oregonlegislature.gov host did not respond to the automated link check from the machine that ran it, so this URL is unconfirmed and is recorded as unverifiable rather than broken. It is the canonical citation for the statute; confirm it in a browser.'
    accessed: '2026-09-27'
  - title: 'California Civil Code Title 1.81.5'
    url: 'https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&chapter=20.&part=4.&law_code=CIV&title=1.81.5.'
    publisher: 'California Legislative Information'
    kind: 'government'
    accessed: '2026-09-27'
tags: ['data-protection', 'united-states', 'data-broker']
related:
  guides: ['privacy-basics/what-privacy-means']
  archive: ['privacy-laws/ccpa-cpra']
  news: []
---

## Why a single national law has not happened

There is no comprehensive federal US consumer privacy statute. Sectional rules exist for
health (HIPAA), financial services (GLBA), and children (COPPA), and they predate the
state wave. Everything general-purpose is state law.

## The statutes, in enactment order

| State                  | Act                          | Enacted            | Effective                              |
| ---------------------- | ---------------------------- | ------------------ | -------------------------------------- |
| California             | CCPA, as amended by the CPRA | 2018, amended 2020 | 1 January 2020, amended 1 January 2023 |
| Virginia               | Virginia CDPA                | 2020               | 1 January 2023                         |
| Colorado               | Colorado Privacy Act         | 2021               | 1 July 2023                            |
| Connecticut            | Connecticut Data Privacy Act | 2022               | 1 July 2023                            |
| Utah                   | Utah Consumer Privacy Act    | 2023               | 31 December 2023                       |
| Oregon                 | Oregon Consumer Privacy Act  | 2023               | 1 July 2024                            |
| Texas, Florida, others | Various                      | 2023 onward        | Varies                                 |

:::note
This table records the enacting acts and their original effective dates. Statutes have been
amended since, and the effective dates in the table should not be read as current law.
Follow the linked state code sections for the operative text.
:::

## Where they differ

The differences are not cosmetic, and a compliance plan written for one state will often
be wrong for the next:

1. **Definition of sale versus sharing.** Colorado and Connecticut both use "sale" and
   "targeted advertising"; others use "sale or sharing" and treat cross-context
   behavioural advertising as sharing.
2. **Sensitive data and consent.** Some states require opt-in consent for sensitive data;
   others require only a right to opt out. Colorado's universal opt-out mechanism for
   sale of sensitive data has no direct equivalent elsewhere.
3. **Children.** Age thresholds vary, and the definitions of "child" and "minor" are not
   consistent across the states.
4. **Private right of action.** Some statutes provide one, with a cure period and limited
   damages; others provide no private right of action and rely entirely on regulatory
   enforcement.
5. **Thresholds and exemptions.** Revenue or record-count thresholds differ, and the
   exemptions for HIPAA, GLBA, and nonprofits are not identical.
6. **Racial profiling.** A small number of states added a specific prohibition on using
   race or ethnicity in profiling decisions, which is unusual among general privacy
   statutes.

## What this means in practice

For a person trying to use the rights, the practical differences are: which state law
covers the business you are dealing with, whether the business must respond to a request
without asking you to identify yourself, and how long the response may take. All of these
vary. A single "privacy request" template is not portable across states.

For an organisation, geofenced compliance is the usual approach: apply the strictest
substantive standard across all covered states. The differences in drafting are what make
that approach imperfect rather than impossible.

## Sources

The primary records are the state code sections linked above. They are the authoritative
texts; summaries of the state-law landscape change frequently and should not be relied on
in place of the statutes.

- [Virginia, Title 59.1 Chapter 52](https://law.lis.virginia.gov/vacode/title59.1/chapter52/)
- [Colorado, SB21-190](https://leg.colorado.gov/bills/sb21-190)
- [Connecticut, Chapter 743jj](https://www.cga.ct.gov/current/pub/chap_743jj.htm)
- [Utah, Title 13 Chapter 61](https://le.utah.gov/xcode/Title13/Chapter61/13-61.html)
- [Oregon, ORS Chapter 646A](https://www.oregonlegislature.gov/bills_laws/ors/ors646A.html)
- [California Civil Code Title 1.81.5](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&chapter=20.&part=4.&law_code=CIV&title=1.81.5.)
