---
title: 'What OPSEC Is: Operational Security and the Five-Step Process'
description: 'OPSEC is a process for denying an adversary information about your intentions and capabilities. What the five steps are, and where OPSEC stops and ordinary security work begins.'
category: 'threat-modeling'
difficulty: 'introductory'
added: '2026-10-05'
updated: '2026-10-05'
author: 'Archive-Opsec contributors'
tags: ['opsec', 'threat-model', 'risk-management', 'security']
featured: true
status: 'published'
sources:
  - title: 'JP 3-13.3, Operations Security'
    url: 'https://media.defense.gov/2020/Oct/28/2002524944/-1/-1/0/JP%203-13.3-OPSEC.PDF'
    publisher: 'U.S. Department of Defense'
    kind: 'government'
    note: 'Joint publication defining OPSEC and the five-step process.'
    accessed: '2026-10-05'
  - title: 'DoDD 5205.02E, DoD Operations Security (OPSEC) Program'
    url: 'https://www.esd.whs.mil/portals/54/documents/dd/issuances/dodd/520502e.pdf'
    publisher: 'U.S. Department of Defense'
    kind: 'government'
    accessed: '2026-10-05'
  - title: 'DoDM 5205.02, DoD Operations Security (OPSEC) Program Manual'
    url: 'https://www.esd.whs.mil/portals/54/documents/dd/issuances/dodm/520502m.pdf'
    publisher: 'U.S. Department of Defense'
    kind: 'government'
    note: 'Set out the five elements as steps and how to rate each one.'
    accessed: '2026-10-05'
  - title: 'National Security Decision Directive Number 298'
    url: 'https://irp.fas.org/offdocs/nsdd298.htm'
    publisher: 'Federation of American Scientists'
    kind: 'academic'
    note: 'Full text of NSDD 298, which formalised the five-step process.'
    accessed: '2026-10-05'
  - title: 'OPSEC Awareness for Military Members, DoD Employees, and Families (GS130)'
    url: 'https://www.cdse.edu/Portals/124/Documents/student-guides/GS130-guide.pdf'
    publisher: 'Center for Defense Studies Security Education'
    kind: 'government'
    note: 'Plain-language teaching version of the same five steps.'
    accessed: '2026-10-05'
related:
  guides:
    [
      'threat-modeling/define-your-threat-model',
      'threat-modeling/common-threats',
      'threat-modeling/opsec-indicators',
    ]

  archive: []
  news: []
---

Operational security — OPSEC — is the practice of denying an adversary information about
your intentions, capabilities and activities. The word *operational* is the part people
skip. It is not a list of things not to say, and it is not security hardening. It is a
process for working out what an opponent could piece together from what you do, and then
changing what you do.

This guide covers what that process actually is, because most public "OPSEC advice" is a
checklist that stops before the reasoning and is therefore useless.

## The definition that matters

US military doctrine is unusually precise here, and the precision is the useful part.
JP 3-13.3 defines three terms that carry the whole discipline:

- **Critical information** — the specific facts about friendly intentions, capabilities
  and activities that an adversary needs in order to plan and act effectively against you.
- **Indicators** — observable actions and publicly available information that can be
  interpreted or pieced together to derive that critical information.
- **Vulnerability** — the condition in which your actions produce indicators that an
  adversary can collect and evaluate in time to act on.

Note what is *not* in that list. Critical information is defined relative to an adversary's
needs, not by how sensitive it feels to you. Your date of birth is not critical information
because nobody plans an operation around it. The date you ship, the quarter you hire, the
building you move into — those are, if an adversary needs them.

This is the first correction most people need: **stop protecting information because it is
private, and start protecting the specific facts that would help someone against you.**

## The five-step process

The process has been formally fixed since NSDD 298 in 1990s-era doctrine, and it appears in
essentially the same form in current DoD instructions. The five steps:

1. **Identify critical information.** Build a list. In doctrine this is a Critical
   Information List, and DoD guidance insists that people from every functional area
   contribute, because administrative and support staff often hold the revealing facts that
   operators do not realise they hold.
2. **Analyse threats.** Who is the adversary, what can they collect, and what do they
   already know? Doctrine's threat analysis includes the collection capabilities of
   potential adversaries, and the striking part is how much of that capability is just
   public data.
3. **Analyse vulnerabilities.** Which of your actions generate indicators, and which of
   those indicators would actually reach the adversary? Both halves matter — an indicator
   nobody can obtain is not a vulnerability.
4. **Assess risk.** Combine value, threat and vulnerability into a judgement about
   likelihood and consequence. DoDM 5205.02 supplies rating tables for exactly this.
5. **Apply countermeasures.** Change the action so the indicator does not exist, or exists
   only among things already public. Countermeasures are ranked by effectiveness against
   the specific vulnerability identified, not by how much they cost or how impressive they
   look.

DoD guidance is explicit that the steps need not be followed in order, but that all five
elements must be present for the analysis to count. A partial pass is a guess.

## Indicators and aggregation

The single most useful idea in the doctrine is that **indicators aggregate**. A data centre
announcing a new 40,000-square-metre facility in a city where you have no presence is not
critical information. A job posting for a named role, a tender document, a conference
appearance and an equipment purchase in the same quarter, all consistent with each other,
is.

That is why step 3 asks what indicators the adversary can *actually collect*. The test is
not "could this reveal something" but "would this arrive in the hands of someone who is
already paying attention". A great deal of what people treat as hidden is published in
plain sight and simply never connected.

See [indicators and critical information](/guides/threat-modeling/opsec-indicators/) for
worked examples of how separate innocuous details become a picture.

## Where OPSEC ends and ordinary security begins

OPSEC and information security are routinely confused, and conflating them produces the
wrong priorities.

- **OPSEC** asks what can be inferred from your *behaviour*, and changes the behaviour.
- **Information security** asks what can be done if someone *already has* the data, and
  hardens the systems.

Encrypting a disk is information security. Not announcing the disk exists until you need to
is OPSEC. Both are legitimate; they answer different questions and neither substitutes for
the other. A countermeasure in one category does not discharge a vulnerability in the
other, which is why a threat model that only produces security purchases has not finished
its work.

There is also a limit worth stating. OPSEC protects against inference by people who are
already looking. It does not protect against an adversary with lawful access to you, and it
cannot protect information you disclose directly. If the realistic adversary is a search
warrant, an employer with read access to your accounts, or someone in the room, then
integrity and access control are the relevant controls, not indicator discipline.

## Doing this outside a military context

The doctrine is written for organisations with planning cycles and adversary estimates. The
method still transfers, with two adjustments.

The first is that **your adversary is usually not a state.** For an individual, the realistic
collector is a data broker, an ad network, an employer, a future employer, a fraudster, an
abusive ex-partner, or an acquaintance who is merely attentive. That changes which steps
you emphasise. Step 2 becomes less about signals intelligence and more about asking who
commercially buys the kind of data you generate — which is a question with a concrete answer
rather than an estimate.

The second is that **most individuals have no organisation behind them**, so there is nobody
to run the process. That is an argument for writing it down, not for skipping it. The
existing guide on [defining a threat model](/guides/threat-modeling/define-your-threat-model/)
covers the written form; the discipline here is only useful if the list of critical
information is specific enough that you could check your own behaviour against it.

## What to read next

- [Indicators and critical information](/guides/threat-modeling/opsec-indicators/) — the
  aggregation problem in worked examples.
- [Define your threat model](/guides/threat-modeling/define-your-threat-model/) — the
  written artefact, for individuals.
- [Common threats](/guides/threat-modeling/common-threats/) — what the adversary actually is
  in civilian contexts.
