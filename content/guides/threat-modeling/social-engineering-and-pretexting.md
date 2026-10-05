---
title: 'Social Engineering and Pretexting: The Attack That Uses Your Own Truths'
description: 'Social engineering exploits what an adversary already knows about you. How pretexting works, why verification beats suspicion, and which channels to distrust for an identity challenge.'
category: 'threat-modeling'
difficulty: 'intermediate'
added: '2026-10-05'
updated: '2026-10-05'
author: 'Archive-Opsec contributors'
tags: ['opsec', 'phishing', 'security', 'account-security', 'threat-model']
status: 'published'
sources:
  - title: 'Avoiding Social Engineering and Phishing Attacks'
    url: 'https://www.cisa.gov/news-events/news/avoiding-social-engineering-and-phishing-attacks'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-10-05'
  - title: 'Phishing Guidance: Stopping the Attack Cycle at Phase One'
    url: 'https://www.cisa.gov/sites/default/files/2023-10/Phishing%20Guidance%20-%20Stopping%20the%20Attack%20Cycle%20at%20Phase%20One_508c.pdf'
    publisher: 'CISA, NSA, FBI and MS-ISAC'
    kind: 'government'
    accessed: '2026-10-05'
  - title: 'How to: Avoid Phishing Attacks'
    url: 'https://ssd.eff.org/module/how-avoid-phishing-attacks'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    accessed: '2026-10-05'
  - title: 'How to Recognize and Avoid Phishing Scams'
    url: 'https://consumer.ftc.gov/articles/how-recognize-and-avoid-phishing-scams'
    publisher: 'Federal Trade Commission'
    kind: 'government'
    accessed: '2026-10-05'
related:
  guides: ['threat-modeling/what-is-opsec', 'authentication/account-recovery', 'authentication/two-factor-authentication', 'threat-modeling/common-threats']
  archive: []
  news: []
---

Social engineering is an attack that uses information you thought was neutral. This guide
covers the mechanism, because the practical defence is not vigilance — it is a rule about
how identity is checked.

## What makes it different

Every other attack on you targets a system. Social engineering targets a *person*, and it
works because the person is following reasonable rules: answering email, taking phone
calls, opening a document that came from a name they recognise.

Two properties make it effective.

**It uses your own OPSEC output.** This is the link to the rest of this section: the same
public details that make you a good candidate for [indicator aggregation](/guides/threat-modeling/opsec-indicators/)
are the raw material for a pretext. A convincing phone call does not require guessing your
employer; it requires knowing it, and quite often you published it. OPSEC reduces the
quality of the intelligence available for social engineering. It does not replace any
control.

**It arrives on a channel you trust for a different purpose.** A phone number on a company
site is evidence a call came from the company, for people who are not being socially
engineered. Phones, SMS, email addresses and caller ID are all trivially spoofable, and
none of them are authentication.

## Pretexting

A **pretext** is a fabricated but plausible context used to justify a request. It is the
social engineering technique that does most of the work in practice, and it usually follows
a recognisable shape:

1. **Establish credibility cheaply.** A name, a project, a mutual contact, or a reference
   to something genuinely public about you.
2. **Create urgency or authority.** A deadline, an executive, a compliance requirement.
   The window for verification is deliberately short.
3. **Ask for something small.** A confirmation, a code, a link click, a name. Small asks
   are deniable and build the pretext's credibility.
4. **Escalate.** The small ask was a credential, or the pretext was for access already
   established in step 3.

Step 4 is where accounts are lost. The request that matters was usually not the first one.

## What actually works

Suspicion is not a control. It degrades, it is not reproducible across people, and it fails
open when someone is tired. CISA's guidance on phishing is consistent on the point: the
defence is a procedure, not a feeling.

The controls that hold up:

- **Verify on a channel you chose, not one the request supplied.** If a call asks you to
  confirm something, hang up and use the number in your own records. This defeats step 1
  and step 2 together, because it removes the attacker from the verification loop.
- **Assume the identifying detail was already public.** A caller who knows your project,
  your employer or your schedule has not proved anything. Treat it as free.
- **Never move authentication to another channel because a message asked you to.** This
  single rule stops most account takeover, because it removes the token request.
- **Make the second factor non-transferrable.** Phishing-resistant hardware keys resist
  this attack because the browser cannot relay them. See
  [passkeys](/guides/authentication/passkeys/) and
  [security keys](/guides/authentication/security-keys/); TOTP codes can be relayed by a
  proxy page, so they are materially weaker against a targeted attacker.
- **Have a recovery path you control.** Account recovery is a pretext target, often a
  weaker one than login. [Account recovery](/guides/authentication/account-recovery/) covers
  securing it.
- **Expect the breach.** The intelligence in a good pretext frequently came from a
  published dataset. DoD threat analysis has always noted that the collection capability in
  question is mostly open-source data; the modern equivalent is a data broker.

## The asymmetry to be honest about

The attacker can spend unlimited time on a target. You cannot. That is why the defence is
built from procedures that are cheap for you and expensive for them — an out-of-band check
costs you one lookup; convincing a pretext costs them sustained effort that most targets do
not justify.

It also means the rational posture is not to become harder to reach. It is to become *harder
to act on once reached*. Someone who knows you work on a specific topic cannot use that
unless they also have a way to authenticate as you, and that is a system property you can
change.

## What to do when it happens

If you have entered credentials or approved an authentication prompt:

1. **Revoke the session, not just the password.** Changing a password does not invalidate
   an already-issued token or cookie. Sign out everywhere, then change the password.
2. **Check recovery details and forwarding rules immediately.** These are the most common
   persistence route and are not touched by a password change.
3. **Revoke third-party access.** Check what applications are authorised on the account and
   remove anything unfamiliar.
4. **Then work out what was used against you,** and note it in your
   [threat model](/guides/threat-modeling/define-your-threat-model/). If a pretext
   succeeded, the information it leaned on is an indicator you had not accounted for.
