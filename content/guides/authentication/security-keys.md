---
title: 'Security keys and phishing-resistant sign-in'
description: 'How hardware-backed public-key credentials protect accounts, and what recovery planning still requires.'
category: 'authentication'
updated: '2026-09-27'
added: '2026-09-27'
author: 'Archive-Opsec contributors'
contributors: []
difficulty: 'intermediate'
tags: ['passkeys', 'authentication', 'phishing', 'security-keys']
featured: false
status: 'published'
sources:
  - title: 'Web Authentication API'
    url: 'https://www.w3.org/TR/webauthn-3/'
    publisher: 'World Wide Web Consortium'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'FIDO2 technical overview'
    url: 'https://fidoalliance.org/fido2/'
    publisher: 'FIDO Alliance'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides: ['authentication/passkeys', 'authentication/two-factor-authentication', 'password-managers/using-a-password-manager']
  archive: []
  news: []
---

## What a security key changes

A security key uses public-key cryptography. The private key stays with the authenticator and the
website receives a public key and a signed response. During sign-in, the credential is scoped to the
website origin, which makes a copied password or a convincing look-alike domain much less useful to
an attacker.

This is different from receiving a code by SMS or email. Those codes can still be useful as a
fallback, but they depend on another account or communication channel that may itself be attacked.

## Register more than one

Register at least two authenticators where the service allows it. Keep one available for daily use
and another in a separate safe location. A single key is a strong sign-in factor but also a single
physical point of failure.

## Recovery is part of authentication

Before enabling a security key, read the service's recovery process. Record recovery codes offline,
understand whether account recovery can bypass the key, and decide who can access the recovery
material. A recovery flow that depends on an old phone number or an unsecured email account can
become the weakest factor.

:::warning
Never register a security key on a device you do not control. A website cannot tell you that a
malicious browser extension did not interfere with the rest of your session.
:::

## Practical order

Use a password manager for a unique account password, enable a security key or passkey, save
recovery codes offline, and review active sessions. Remove old authenticators when a device or key
is permanently lost.
