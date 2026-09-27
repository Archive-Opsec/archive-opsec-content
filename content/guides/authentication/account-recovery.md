---
title: 'Account recovery is part of account security'
description: 'How recovery email, phone numbers, codes, trusted devices and support processes can become the weakest path into an account.'
category: 'authentication'
updated: '2026-09-27'
added: '2026-09-27'
author: 'Archive-Opsec contributors'
contributors: []
difficulty: 'intermediate'
tags: ['authentication', 'account-recovery', 'password-manager', 'threat-model']
featured: false
status: 'published'
sources:
  - title: 'Digital Identity Guidelines: Authentication and Lifecycle Management'
    url: 'https://pages.nist.gov/800-63-4/sp800-63b.html'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'More than a Password'
    url: 'https://www.cisa.gov/mfa'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-09-27'
related:
  guides: ['authentication/security-keys', 'authentication/passkeys', 'password-managers/using-a-password-manager']
  archive: []
  news: []
---

## The recovery path is a login path

People often secure the primary login and forget the recovery flow. An attacker who cannot guess
your password may still try to take over the recovery email, intercept a code, convince support to
change the account, or use an old trusted device.

List every recovery method an account offers. Include recovery email, phone number, backup codes,
trusted browsers, authenticator apps, security keys, identity questions and support escalation.
Treat each one as an authentication factor with its own threat model.

## Build recovery before you need it

Use a dedicated recovery email with a unique password and strong authentication. Store recovery
codes in an encrypted password manager and an offline backup. Register more than one security key
when the service permits it, but keep the spare key separate from the daily device.

Do not use answers to public identity questions. If a service requires them, use random values and
store them like passwords. Remove phone numbers or old devices that no longer serve a clear recovery
purpose.

## Test the process

Read the recovery instructions while you are still signed in. Confirm which factor is needed, how
long a lockout lasts, whether changing a password revokes sessions, and whether an attacker can add
a new recovery method before the legitimate owner notices.

:::warning
Never send recovery codes, password-manager exports or security-key PINs to someone claiming to be
support. A legitimate support process should not require your secret authentication material.
:::
