---
title: 'Passkeys'
description: 'What public-key credentials change, where they currently hurt, and whether to adopt them now.'
category: 'authentication'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['passkeys', 'authentication', 'end-to-end-encryption', 'key-management']
status: 'published'
sources:
  - title: 'Web Authentication: An API for accessing Public Key Credentials Level 3'
    url: 'https://www.w3.org/TR/webauthn-3/'
    publisher: 'W3C'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Web Authentication: An API for accessing Public Key Credentials Level 2'
    url: 'https://www.w3.org/TR/webauthn-2/'
    publisher: 'W3C'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Passkey Developer Documentation'
    url: 'https://passkeys.dev/'
    publisher: 'FIDO Alliance'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'RFC 8555: A Certificate Authority-Vouched OAuth 2.0 Public Client Grant'
    url: 'https://www.rfc-editor.org/rfc/rfc8555'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
related:
  guides:
    [
      'authentication/two-factor-authentication',
      'encryption/key-management',
      'password-managers/using-a-password-manager',
    ]
  archive: []
  news: []
---

A passkey is a cryptographic key pair that replaces the password. The private key stays
on your device, in a secure element or a platform credential store; the public key is
registered with the service. Logging in means proving possession, not proving knowledge.

## Why this is a real improvement

**Phishing stops working.** The credential is bound to an origin. A page at
`evil-example.com` cannot present a credential registered for `example.com`, so a
perfectly convincing clone of a login page harvests nothing.

**There is no secret to reuse or leak.** A database breach exposes public keys, which are
not secret and not useful. The class of [credential stuffing](/archive/data-breaches/collection-one/)
effectively disappears for passkey accounts.

**No shared secret to phish.** There is nothing for a proxy to relay, so a real-time
phishing proxy cannot produce a valid challenge response.

**Nothing to type, nothing to reuse.** The friction that caused people to work around
password managers largely goes away.

:::note
This is the closest thing to a straight upgrade in this entire guide, and it removes the
user-visible complexity that made previous security improvements fail to be adopted. The
caveats below are about ecosystem maturity rather than about the cryptography.
:::

## How it works, briefly

1. The site issues a challenge scoped to its origin.
2. Your authenticator signs it with a private key held in a secure element, after a user
   verification step — a fingerprint, a face, a device PIN.
3. The site verifies the signature against the registered public key.

The private key never leaves the authenticator and is not exportable, which is what makes
device loss a real risk.

## Where it currently hurts

**Account recovery is the weak point.** If every device holding your passkeys is lost,
recovery is the one thing passkeys were supposed to remove. In practice this means:

- platform-bound passkeys depend entirely on the platform account's recovery
- hardware keys are the strongest option, and you need two of them, stored separately
- sync-based passkeys introduce a company into the trust chain that was supposed to leave

**Cross-platform movement is immature.** Moving from one ecosystem to another is still
awkward, and this is the main reason adoption is uneven.

**Shared and work accounts are poor fits.** Anyone with the credential can authenticate;
there is no way to say "read only", and no per-person revocation short of regenerating.

**Enterprise attestation features have privacy trade-offs.** Device posture and
organisation binding can be valuable for a company and a data source for anyone
else.

:::warning
Adopt passkeys for personal accounts incrementally, and keep your password and recovery
codes working until you have tested recovery on a second device. Abandoning the
password before you have confirmed the recovery path is how people lose accounts.
:::

## Adoption advice

1. Enable passkeys where offered, keeping the password as a fallback initially.
2. Register a hardware key as a second method on anything high-value.
3. Test recovery on a device that is not the one you registered on.
4. Store any recovery codes in your password manager.
5. Expect the support experience to be worse than password login for a while. It is
   early.

## Sources

- [Web Authentication Level 3](https://www.w3.org/TR/webauthn-3/) — the current
  specification, including resident credentials and attestation policies.
- [Web Authentication Level 2](https://www.w3.org/TR/webauthn-2/) — the level most
  deployed today, useful for understanding what is actually implemented.
- [FIDO passkey developer documentation](https://passkeys.dev/) — the ecosystem's own
  description of synchronisation, device binding, and recovery.
- [RFC 8555](https://www.rfc-editor.org/rfc/rfc8555) — PKCE, the related mechanism that
  stops an authorisation code being redeemed by the wrong client.
