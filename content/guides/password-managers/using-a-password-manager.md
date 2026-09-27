---
title: 'Using a Password Manager'
description: 'Why password reuse is the main threat, what to look for in a manager, and how to migrate without a lockout.'
category: 'password-managers'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['password-manager', 'encryption', 'open-source']
featured: true
status: 'published'
sources:
  - title: 'NIST SP 800-63B: Digital Identity Guidelines'
    url: 'https://pages.nist.gov/800-63-3/sp800-63b.html'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Bitwarden Security Whitepaper'
    url: 'https://bitwarden.com/help/bitwarden-security-white-paper/'
    publisher: 'Bitwarden'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'Passphrase Entry in GNOME Keyring and KeePassXC'
    url: 'https://keepassxc.org/docs/'
    publisher: 'KeePassXC'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides:
    [
      'authentication/two-factor-authentication',
      'authentication/passkeys',
      'encryption/key-management',
    ]
  archive: []
  news: []
---

A password manager is the highest-value security change available to almost everyone, and
it is not a privacy measure. That is worth saying plainly, because password advice gets
buried under privacy advice and therefore ignored.

## Why reuse is the problem

Attackers do not guess passwords. They take credentials from one breach and try them
everywhere, because the probability that a given person's password is reused somewhere
else is high enough to make it profitable. A
[breach corpus](/archive/data-breaches/collection-one/) assembled from thousands of
services is not a set of passwords you could brute-force; it is a lookup table.

[Collection #1](/archive/data-breaches/collection-one/) is the reference case: a set of
credential pairs across millions of accounts, offered for sale. Its existence is the
argument for unique passwords, in a way no statistic about password strength is.

:::note
NIST's guidance is explicit on several points that common advice gets wrong: permit
paste and password managers into password fields, do not impose arbitrary composition
rules, do not require periodic rotation without evidence of compromise, and check
memorised secrets against a blocklist of known-breached passwords. See SP 800-63B.
:::

## What to look for

**Zero-knowledge architecture.** The vault is encrypted on your device with a key derived
from your master password, and the server only ever sees ciphertext. This is the single
most important design property, and it is the one that is easiest to claim falsely.

**Open source client and server.** Both halves matter: the client touches your keys, the
server is the thing you are trusting not to be compelled.

**An independent audit.** A cryptographic design that has never been reviewed is a
hypothesis. Treat vendor-published audits as meaningful and blog posts as marketing.

**A real recovery story.** Encrypted export files you can re-import elsewhere. If there
is no export, you have a single point of failure with no recourse.

**Self-hosting, if you can run a server.** Bitwarden and KeePassXC both support it. This
is worth the effort for a technical user and is not worth it for most people.

**No forced account.** A zero-knowledge provider cannot reset your master password, which
is the point, and which also means an emergency requires your recovery material.

## The master password

The master password protects the vault, so it must not be in the vault. It should be
long, memorable, and unique:

- Four or five unrelated words is stronger than a short complex string you will forget.
- Never reuse it anywhere else.
- Do not rotate it on a schedule. Rotate it if you think it is exposed.
- A passphrase is fine on a phone with a secure element, and marginal on a desktop where
  a keylogger is a realistic concern.

## Migrating without a lockout

1. Install the manager, create the vault, and **write down the recovery kit first**.
2. Confirm you can unlock the vault on a second device before changing anything.
3. Export the encrypted recovery file and store it somewhere you will not lose it.
4. Start with the account that can reset every other account: your email provider.
5. Then financial, then identity, then everything else.
6. Do not log out of the old password manager until the new one is fully populated.
7. Save each service's second-factor recovery codes as you go. See
   [two-factor authentication](/guides/authentication/two-factor-authentication/).

:::warning
The most common self-inflicted lockout is losing the master password or the recovery
material during migration, not an attack. Do step 3 and then genuinely verify step 2.
:::

## Is a password manager private?

A password manager knows which services you have accounts with, which is a sensitive
social graph, and it is a high-value target: it is the one place every credential is
together. A zero-knowledge design reduces this to a target that yields a ciphertext blob
and nothing else — but it remains the most sensitive application you run. Protect it the
way you would protect a hardware token, and keep the second copy of your recovery
material somewhere that is not the same device.

## Sources

- [NIST SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html) — current federal
  guidance on password storage, composition, and rotation.
- [Bitwarden security whitepaper](https://bitwarden.com/help/bitwarden-security-white-paper/) — a
  vendor description of its zero-knowledge design, including the derivation parameters.
- [KeePassXC documentation](https://keepassxc.org/docs/) — the offline, file-based
  alternative, and its key derivation settings.
