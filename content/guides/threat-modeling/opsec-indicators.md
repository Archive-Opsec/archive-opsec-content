---
title: 'OPSEC Indicators and Critical Information: How Details Aggregate'
description: 'Harmless details become a picture when combined. How to build a critical information list, spot the aggregation problem, and test whether an indicator would actually reach an adversary.'
category: 'threat-modeling'
difficulty: 'intermediate'
added: '2026-10-05'
updated: '2026-10-05'
author: 'Archive-Opsec contributors'
tags: ['opsec', 'threat-model', 'metadata', 'risk-management']
status: 'published'
sources:
  - title: 'JP 3-13.3, Operations Security'
    url: 'https://media.defense.gov/2020/Oct/28/2002524944/-1/-1/0/JP%203-13.3-OPSEC.PDF'
    publisher: 'U.S. Department of Defense'
    kind: 'government'
    note: 'Defines indicators and the condition of vulnerability.'
    accessed: '2026-10-05'
  - title: 'DoDM 5205.02, DoD Operations Security (OPSEC) Program Manual'
    url: 'https://www.esd.whs.mil/portals/54/documents/dd/issuances/dodm/520502m.pdf'
    publisher: 'U.S. Department of Defense'
    kind: 'government'
    accessed: '2026-10-05'
  - title: 'Surveillance Self-Defense: Your Security Plan'
    url: 'https://ssd.eff.org/module/your-security-plan'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    accessed: '2026-10-05'
  - title: 'Why Metadata Matters'
    url: 'https://ssd.eff.org/module/why-metadata-matters'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    note: 'How innocuous fields combine into a profile.'
    accessed: '2026-10-05'
related:
  guides: ['threat-modeling/what-is-opsec', 'metadata/metadata-explained', 'threat-modeling/define-your-threat-model']
  archive: []
  news: []
---

The central claim of operational security is not that any single fact is dangerous. It is
that **a set of individually unremarkable facts is dangerous in aggregate**, and that the
aggregation happens in someone else's analysis, not in yours. This guide is about building
the list, spotting the pattern, and applying the test that catches most over- and
under-correction.

## Critical information is relative, not sensitive

Doctrine's definition of critical information is worth repeating because it is easy to get
backwards: critical information is the set of facts an adversary needs to plan and act
against you. It is defined by *their requirement*, not by your attachment to the data.

The practical consequence is that your instinct to protect the most personal data is
usually misdirected. The exact text of a medical appointment may be private and irrelevant
to any adversary. The fact that you are relocating on a particular date, funded by a
particular source, to a particular address, is none of those things and may be the whole
picture.

Build the list by working backwards from the adversary's problem rather than forwards from
your data:

1. Write down what you are doing that an opponent would want to stop, delay or exploit.
2. Write down what they would need to know to do it. That is the critical information list.
3. Only then ask what you hold that matches it.

Step one is uncomfortable, because it requires naming the activity as something an adversary
might have an interest in. For most individuals the honest answer is a move, a launch, a
job change, a filing, a diagnosis, or a relationship — and in each case the useful list is
short.

## Indicators are what you do, not what you store

An **indicator** is a detectable action or piece of public information. An **indicator
leak** is that indicator becoming available to the adversary. The distinction matters
because most data minimisation advice stops at the first noun.

- **Metadata** is data about data: timestamps, file sizes, revision history, co-occurrence.
- **Behaviour** is what you do: when you use a service, from where, in what pattern.
- **Disclosure** is what you say: to whom, in what forum.

Metadata and behaviour are where OPSEC has the most to say, because they are generated
constantly and nobody decides to create them. [Metadata fundamentals](/guides/metadata/metadata-explained/)
covers the mechanics; the OPSEC question is always which of these an adversary could
actually obtain.

## The aggregation problem

Here is a worked example. None of these is a disclosure:

| Detail | Ordinarily meaningful? |
| --- | --- |
| A conference accepts a paper on database replication | No |
| You post about "excited to share" | No |
| A grant is awarded to your institution, same quarter | No |
| The paper is on exactly the system your institution just received funding for | No |
| A well-known researcher cites your work in the same month | No |

Each row is defensible on its own. Combined, they describe a specific technical direction,
a specific capability, a specific person and a specific time. Doctrine treats this as a
single vulnerability, and the countermeasure is not secrecy about any one item — it is
breaking the *consistency* between them.

This is why OPSEC countermeasures frequently look like "stagger things" or "post something
else first". Those are not superstition. Dispersal works because it reduces what an adversary
can correlate.

## The test that prevents both errors

After listing candidate indicators, apply a single question to each:

> **Would this actually reach someone who is already paying attention?**

Two failure modes disappear at once:

- **Over-correction** — removing something because it "reveals" you, when the only people
  who would ever see it could not connect it to anything. This is the source of most
  self-defeating paranoia: skipped conferences, deleted accounts, and abandoned projects
  that were protecting against an adversary that does not exist for that particular reader.
- **Under-correction** — assuming a detail is unremarkable because it is boring in
  isolation. Almost every indicator is boring in isolation. That is what makes correlation
  the threat.

If the answer is no, the countermeasure buys nothing and costs you something real. If the
answer is yes, the indicator is part of the problem regardless of how innocent it looks
alone.

## Working the list for an individual

For most people the list converges quickly onto a small number of channels, and it is
worth writing yours down before deciding on any tool. In rough order of how much they
usually matter:

1. **Timeline convergence.** Several independent channels each carrying one part of the
   same fact. Address changes, employer changes, and public posts about both.
2. **Location metadata.** Photographs and posts that carry coordinates or a recognisable
   background at a sensitive time.
3. **Audience assumption.** Posting that is public in fact being read by a specific person
   you did not intend as an audience — an employer, a family member, a school, a court.
4. **Third-party accumulation.** Data you never gave to anyone, assembled by a broker,
   an ad network, or a breached dataset you did not know existed.

Note that only the fourth requires a technology answer. The first three are behavioural and
are resolved by choosing what to publish, which is why OPSEC cannot be bought.

## The cost side

Countermeasures are not free, and DoD guidance ranks them against the specific vulnerability
rather than by cost or appearance. For an individual the costs are usually:

- **Attention.** Every measure is a recurring decision, and recurring decisions get dropped.
- **Opportunity.** Not attending, not publishing, not saying — these cost something real.
- **Signal.** A conspicuously quiet account is itself an indicator, for anyone modelling you.

That last point is the one most self-help OPSEC material omits. A decision that is easy to
reverse and hard to explain is usually the right one to prefer, and the list should be short
enough that you will still be following it in a year.
