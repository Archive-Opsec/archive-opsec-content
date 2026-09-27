---
title: 'Key Management'
description: 'The part of cryptography that actually determines whether it helps: who holds keys, where, and for how long.'
category: 'encryption'
difficulty: 'advanced'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['key-management', 'encryption', 'end-to-end-encryption', 'open-source']
status: 'published'
sources:
  - title: 'NIST SP 800-57 Part 1 Rev. 5: Key Management'
    url: 'https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'RFC 8446: TLS 1.3'
    url: 'https://www.rfc-editor.org/rfc/rfc8446'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Passkey Developer Documentation'
    url: 'https://passkeys.dev/'
    publisher: 'FIDO Alliance'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides:
    [
      'encryption/encryption-explained',
      'authentication/passkeys',
      'password-managers/using-a-password-manager',
      'operating-systems/full-disk-encryption',
    ]
  archive: ['security-incidents/xz-utils-backdoor']
  news: []
---

Encryption is a solved problem. Key management is not, and it is where every serious
failure happens. This page is about the second one.

## Four questions to ask about any key

1. **Who can use it?** Which humans, which services, which devices.
2. **Where does it live?** A hardware secure element, a file, an environment variable, a
   memory buffer.
3. **How long does it exist?** Created, rotated, expired, destroyed — and what "destroyed"
   means when copies exist in backups.
4. **Who can compel its use?** This is the question end-to-end encryption answers, and it
   has a technical answer: if no server holds the key, a legal demand produces ciphertext.

:::note
A system that can reset your password, or that decrypts your data on request, holds the
key. Whatever the interface calls it, that is the trust relationship you have accepted.
:::

## Storage, roughly in order of strength

**Hardware secure element.** Non-exportable, tamper-resistant, and only released after the
platform verifies boot integrity. This is what
[passkeys](/guides/authentication/passkeys/) and
[TPM-backed disk encryption](/guides/operating-systems/full-disk-encryption/) use.

**TPM or secure enclave outside the OS.** Attacker with physical access and knowledge of
the platform's state can potentially extract it. Better than a file, worse than an SE.

**Encrypted file on disk.** Protection equals the strength of the passphrase, and the
passphrase is in memory while the session runs. A password manager vault works this way
and it is a reasonable design, provided the client is trustworthy.

**File or environment variable on a general-purpose system.** Anyone with read access to
the account has the key. Fine for development, not for production.

:::warning
"Encrypted at rest" in a product's own marketing usually means the third row, sometimes the
fourth. The question to ask is where the key is stored and who can retrieve it, and a
vendor that cannot answer that question specifically has not thought about it.
:::

## Rotation and expiry

Rotation limits the damage from a single leaked key and is straightforward for symmetric
keys. It is genuinely hard for data-encrypting keys, because every copy of the data
depends on the key that encrypted it.

Practical rules:

- Rotate keys on a schedule that matches the value of the data, not a round number.
- Keep a key version with each ciphertext so old data remains readable.
- On destruction, remember backups. A key destroyed on the live system may exist in a
  snapshot for years.
- Never reuse a key across two purposes. Keys derived for different contexts should not
  be interchangeable.

## Subkeys and derivation

**Key derivation** stretches a passphrase into a key with a deliberately slow function, so
that guessing is expensive. The parameters matter and they age; raise them when the
implementation supports it. Argon2id and scrypt are the current reasonable choices, PBKDF2
is the legacy default.

**Hierarchical keys.** A root key encrypts, or derives, subkeys that do the work. This is
how key rotation is made affordable: you rewrap the subkeys, you do not re-encrypt the
data. NIST's guidance in
[SP 800-57 Part 1](https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final) covers this in
detail.

:::tip
Treat "where is the key" as a question with a written answer kept next to the system, and
revisit it whenever the system is moved, containerised, backed up, or given to a
colleague. Most key exposure happens during ordinary operational changes.
:::

## The failure modes, in order of frequency

1. **A key in a repository, a log, an error message, or a crash dump.** Nearly free to
   prevent with secret scanning.
2. **Keys not rotated after an employee or contractor leaves.**
3. **Backups of everything, forever.** A backup is a second key store with no expiry.
4. **The same key in test and production.** Common, and a test environment is often the
   least protected one.
5. **No revocation.** If you cannot invalidate a key, every leak is permanent.

## Sources

- [NIST SP 800-57 Part 1 Rev. 5](https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final) — the
  key management lifecycle: generation, registration, distribution, storage, usage,
  archive, destruction.
- [RFC 8446](https://www.rfc-editor.org/rfc/rfc8446) — an example of a protocol where key
  schedule design, forward secrecy, and the removal of static RSA and static DH are the
  substantive changes.
- [Passkey documentation](https://passkeys.dev/) — how a non-exportable, device-bound
  credential avoids the distribution problem entirely.
