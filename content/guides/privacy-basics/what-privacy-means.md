---
title: 'What Privacy Actually Means'
description: 'A working definition of privacy, the four kinds people mean, and why the word gets used to sell things.'
category: 'privacy-basics'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['privacy', 'data-minimisation', 'threat-model']
featured: true
status: 'published'
sources:
  - title: 'Surveillance Self-Defense'
    url: 'https://ssd.eff.org/'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    accessed: '2026-09-27'
  - title: 'Data Protection by Design and by Default'
    url: 'https://eur-lex.europa.eu/eli/reg/2016/679/oj'
    publisher: 'European Union'
    kind: 'regulator'
    accessed: '2026-09-27'
related:
  guides: ['threat-modeling/define-your-threat-model', 'privacy-basics/harm-reduction']
  archive: ['privacy-laws/gdpr']
  news: []
---

Privacy is one of those words that gets used to mean four different things, and most
disagreement about privacy online comes from people quietly meaning different ones.

## Four different things

**Privacy as secrecy.** Nobody should be able to read my messages. This is the part
encryption addresses, and it is the part that is technically easiest to reason about.

**Privacy as context.** What I do should not be public in a form that reveals more than
it needs to. A bank knows my balance; a bank does not need to know my browsing history to
send me a statement. This is _data minimisation_, and it is the part that is hardest to
buy off the shelf.

**Privacy as control.** I should be able to see, correct, and delete what is recorded
about me. This is the substance of rights such as access and erasure, and it is a
property of a _process_, not of a database.

**Privacy as autonomy.** I should be able to act without an audience. Not being watched is
a precondition for doing things that are new, embarrassing, or illegal where you live.

:::note
These four pull in different directions. End-to-end encryption makes secrecy easy and
deletion hard. A search engine with no personal history gives up useful personalisation.
Choosing a tool means choosing which of the four you are optimising for, which is why
[threat modelling](/guides/threat-modeling/define-your-threat-model/) has to come before
any recommendation.
:::

## What privacy is not

Privacy is not the same as anonymity. Anonymity is a stronger property: it means the
action cannot be tied to a person at all. Most people want privacy, not anonymity, and
most privacy tools are sold as if they delivered anonymity. They usually do not.

Privacy is also not secrecy by obscurity. Moving your accounts to new usernames does
nothing if the same profile is reconstructed from your behaviour, your contact list, or a
single forwarded screenshot.

## The trade that is actually being offered

Almost every free service is funded by advertising, which means its business model is to
share an audience description with third parties. A privacy-preserving service is one
that has found some other way to pay, or has decided not to collect the data. Both are
fine outcomes. What is not fine is presenting a data-extracting business model as a
privacy feature.

:::warning
"Privacy-friendly", "encrypted", "anonymous" and "no logs" are marketing words with no
shared definition. Each one should be answerable to a specific document: an encryption
protocol, an audit report, a policy with a named entity, a retention schedule. If a
product page does not link to one, treat the claim as unsubstantiated.
:::

## A workable starting position

You do not need to solve all of this. In rough order of value for most people:

1. Stop credential reuse, and turn on multi-factor authentication
2. Reduce the number of services that hold data about you
3. Turn off location history and ad personalisation where they exist
4. Encrypt the device and the network
5. Worry about adversaries you do not actually have

Steps 1 to 4 are unglamorous and effective. Step 5 is where most online privacy advice
goes, and for most people it is where effort stops being repaid.

## Sources

- [Surveillance Self-Defense](https://ssd.eff.org/) — EFF's threat-modelling guides, the
  best free introduction to thinking about this systematically.

Continue with [harm reduction for beginners](/guides/privacy-basics/harm-reduction/) or
[define your threat model](/guides/threat-modeling/define-your-threat-model/).
