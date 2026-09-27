---
title: 'Harm Reduction for Beginners'
description: 'A short, opinionated reading order that maximises the protection you get per hour spent.'
category: 'privacy-basics'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['privacy', 'digital-footprint', 'password-manager', 'encryption']
status: 'published'
sources:
  - title: 'Surveillance Self-Defense'
    url: 'https://ssd.eff.org/'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    accessed: '2026-09-27'
  - title: 'Online Security'
    url: 'https://consumer.ftc.gov/online-security'
    publisher: 'US Federal Trade Commission'
    kind: 'regulator'
    note: 'Replaces the Security Booklet, whose domain no longer resolves.'
    accessed: '2026-09-27'
  - title: 'Digital Security Helpline'
    url: 'https://www.accessnow.org/help/'
    publisher: 'Access Now'
    kind: 'ngo'
    accessed: '2026-09-27'
related:
  guides:
    [
      'privacy-basics/what-privacy-means',
      'password-managers/using-a-password-manager',
      'authentication/two-factor-authentication',
    ]
  archive: []
  news: []
---

Most privacy advice is written as a list of ideal end states, which makes it useless: you
cannot do all of it, so you do none of it. This page is an ordered subset. Each step is
worth more than everything after it.

## Step 1 — one password manager, unique passwords everywhere

This is the highest-value change available to almost everyone, and it is not a privacy
measure at all, which is why it is often skipped. Credential stuffing turns one leaked
password into breaches at dozens of unrelated services, and the blast radius grows every
time a password is reused.

Move to a manager, generate a unique password for every account, and change the password
on your email account first. See
[using a password manager](/guides/password-managers/using-a-password-manager/).

## Step 2 — multi-factor authentication on the accounts that matter

Prioritise your email provider, your bank, and anything that holds money or identity
documents. Prefer an authenticator app or a hardware key over SMS, which is vulnerable to
SIM swapping. See
[two-factor authentication](/guides/authentication/two-factor-authentication/) and
[passkeys](/guides/authentication/passkeys/).

:::warning
If you switch to a hardware key or an authenticator, save the recovery codes _before_ you
log out. The most common self-inflicted account lockout is losing a second factor, not
being attacked.
:::

## Step 3 — full-disk encryption

A lost or stolen laptop contains your entire life. Turning on BitLocker, FileVault, or
`cryptsetup` on Linux takes a few minutes and removes the most common physical attack
surface there is. Back up the recovery key somewhere that is not the device.

## Step 4 — reduce location and ad history

Location history and advertising identifiers are the two records that follow you across
unrelated services, and both are usually a single setting in a system you already use.
This is where the effort per unit of privacy gain becomes genuinely good.

## Step 5 — a browser that does not fingerprint, and DNS you control

Turning on a browser's built-in resistance to fingerprinting, and moving DNS to an
encrypted resolver you choose, breaks two passive collection paths that operate even when
you are not targeted. See [browser fingerprinting](/guides/browsers/browser-fingerprinting/)
and [DNS privacy](/guides/dns/dns-privacy/).

## Step 6 — messaging you actually need

Move conversations that matter to an end-to-end encrypted channel, and understand that
metadata remains. See
[end-to-end encrypted messaging](/guides/messaging/end-to-end-encrypted-messaging/).

## Step 7 — everything else, only if step 1 has a threat model

Tor, disposable email, burner phones, seeded operating systems, dedicated hardware. These
are real tools with real costs: time, reliability, and the loss of services that assume a
mainstream browser. See
[define your threat model](/guides/threat-modeling/define-your-threat-model/) before
starting here, and only pursue the parts that match a threat you actually have.

## What to skip

- Custom builds of everything, forever. Rebuild cost is real and updates stop applying.
- Any tool that requires you to trust one vendor more than the default you already use,
  for a threat you do not have.
- Privacy settings inside a platform you are going to delete next month.

:::tip
Do the first three steps today. They take under an hour together, they survive a lost
device, and they are the ones you will not regret. Everything else can wait until you have
a reason.
:::
