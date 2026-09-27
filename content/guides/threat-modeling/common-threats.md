---
title: 'Common Threats and Which Ones Deserve Action'
description: 'A ranked list of realistic threats, the control that addresses each, and an honest note on the ones to ignore.'
category: 'threat-modeling'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['threat-model', 'fingerprinting', 'ransomware', 'phishing', 'end-to-end-encryption']
status: 'published'
sources:
  - title: 'Online Security'
    url: 'https://consumer.ftc.gov/online-security'
    publisher: 'US Federal Trade Commission'
    kind: 'regulator'
    note: 'FTC consumer security hub; replaces a dead "Security Planner" URL.'
    accessed: '2026-09-27'
  - title: 'CISA: Cross-Sector Cybersecurity Performance Goals'
    url: 'https://www.cisa.gov/cpg'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'CVE Record: CVE-2021-44228 (Log4Shell)'
    url: 'https://nvd.nist.gov/vuln/detail/CVE-2021-44228'
    publisher: 'National Vulnerability Database'
    kind: 'government'
    accessed: '2026-09-27'
related:
  guides:
    [
      'threat-modeling/define-your-threat-model',
      'browsers/browser-fingerprinting',
      'operating-systems/hardening-basics',
    ]
  archive: ['security-incidents/log4shell', 'security-incidents/heartbleed']
  news: []
---

Threat lists are usually unordered, which makes them useless for deciding what to do
first. This one is ordered by expected loss for an individual, given current conditions.

## 1. Credential reuse and account takeover

Still the most common cause of personal harm. One breached service becomes every service,
through automated credential stuffing.

**Control:** a password manager, unique passwords, and multi-factor authentication on
email and financial accounts. See
[using a password manager](/guides/password-managers/using-a-password-manager/).

## 2. Phishing and session hijacking

Credential theft has largely displaced exploit chains as the initial access route.
Passwords are not the thing being stolen any more; cookies and session tokens are.

**Control:** passkeys or hardware-backed second factors, a mail filter that marks
lookalike domains, and a habit of navigating to services by typing the domain rather than
following a link in a message.

:::warning
Any prompt to approve a login you did not initiate is an attack until proven otherwise.
An MFA prompt you did not trigger means someone has your password already — deny it, then
change that password.
:::

## 3. Unpatched software

Exploitation is rapid after disclosure. The
[Log4Shell](/archive/security-incidents/log4shell/) disclosure is the canonical example of
how short the window can be.

**Control:** automatic updates on the operating system, browser, and router; and
[end-of-life awareness](https://www.cisa.gov/resources-tools/resources/reducing-attack-surface-end-support-edge-devices)
for anything you cannot update, such as a phone whose manufacturer stopped shipping
updates.

## 4. Device theft

A stolen, unlocked phone or laptop is a total compromise of the account session, not just
the device.

**Control:** full-disk encryption, a strong screen lock with short auto-lock, remote
wipe, and device-tracking enabled.

## 5. Fingerprinting and cross-site tracking

Passive, legal, and continuous. Does not require breaking in; it requires a browser with
default settings.

**Control:** resistance to fingerprinting, third-party cookie blocking, and a reduced set
of identifiers. See
[browser fingerprinting](/guides/browsers/browser-fingerprinting/).

## 6. Over-collection by services you use

The largest category by volume of data collected, and the one where you have the most
leverage: turn off location history, ad personalisation, and unnecessary permissions.

## 7. Network observation

A hostile network can see what you resolve, which servers you contact, and how much you
transfer. Usually not who you are.

**Control:** encrypted DNS and TLS, and Tor where the destination matters. See
[DNS privacy](/guides/dns/dns-privacy/) and
[what Tor does and does not protect](/guides/tor/what-is-tor/).

## 8. Supply chain and update compromise

Real, occasionally catastrophic, and mostly out of your hands. The
[xz-utils backdoor](/archive/security-incidents/xz-utils-backdoor/) is the reference
case: a maintainer account compromised, a payload hidden in a test fixture, shipped for
several releases.

**Control:** distribution diversity, reproducible builds, and watching distribution
advisories. You cannot fully mitigate this one.

## 9. Targeted state-level targeting

Real, well documented, and rare. It also drives disproportionate amounts of defensive
advice online.

**Control:** compartmentalisation, a hardened endpoint, strong authentication, and a
threat model that acknowledges the cost. If nobody in your model has already noted that
this threat exists, the model is incomplete.

## What to ignore

- **The idea that a public IP address identifies you.** It often narrows a household or
  workplace, and that is genuinely sensitive, but it is rarely a name.
- **Named attackers you have never heard of with no sources.** Check the
  [archive](/archive/) provenance labels; anything that is a claim rather than a record
  should not change your behaviour.
- **"They know everything."** They know a great deal, unevenly, and structured measures
  work against specific collection methods rather than against "them" in general.
