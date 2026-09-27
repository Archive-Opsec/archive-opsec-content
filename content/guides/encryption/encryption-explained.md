---
title: 'Encryption Explained'
description: 'Encryption in transit and at rest, symmetric and asymmetric primitives, and the misconceptions that make people over- or under-trust it.'
category: 'encryption'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['encryption', 'key-management', 'end-to-end-encryption', 'hardening']
status: 'published'
sources:
  - title: 'RFC 8446: The Transport Layer Security (TLS) Protocol Version 1.3'
    url: 'https://www.rfc-editor.org/rfc/rfc8446'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'NIST SP 800-57 Part 1 Rev. 5: Key Management'
    url: 'https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'NIST SP 800-38A: Recommendation for Block Cipher Modes of Operation'
    url: 'https://csrc.nist.gov/pubs/sp/800/38/a/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
related:
  guides:
    [
      'encryption/key-management',
      'operating-systems/full-disk-encryption',
      'messaging/end-to-end-encrypted-messaging',
      'metadata/metadata-explained',
    ]
  archive: ['security-incidents/heartbleed', 'security-incidents/log4shell']
  news: []
---

Encryption is not one thing. It is a small set of primitives used in different places,
with different parties holding keys and different failure modes. Most confusion about
"is this secure" comes from not knowing which kind is in play.

## The two primitives you need

**Symmetric encryption.** One secret key encrypts and decrypts. Fast, and the right tool
for bulk data. AES in a proper mode is the default choice; see
[NIST SP 800-38A](https://csrc.nist.gov/pubs/sp/800/38/a/final) for the mode choices and
[SP 800-57](https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final) for key policy.

**Asymmetric encryption.** A key pair, one public and one private. The public half
encrypts, the private half decrypts. It is slow, and its real purpose is distribution:
solving the problem of agreeing a shared secret over a channel you do not yet trust.

In practice both are used. TLS 1.3 uses asymmetric cryptography to establish a shared
secret, then symmetric cryptography for the connection.

:::note
Hashing is not encryption. A hash is one-way and has no key. It is used to verify
integrity and to derive keys, and calling it "encryption" is a sign that the explanation
is unreliable.
:::

## The two places it is used

**In transit.** TLS protects a connection from both ends to whoever terminates it. The
security property is not "encrypted" but "encrypted to an authenticated endpoint". If the
endpoint's certificate is validated, a network attacker cannot read or modify the
connection.

:::warning
A certificate warning is a failed authentication, which means an active attacker may be
present. Clicking through is a decision to continue anyway. TLS 1.3 removed the ability
to downgrade silently for this reason — see [RFC 8446](https://www.rfc-editor.org/rfc/rfc8446).
:::

**At rest.** Data is encrypted on the device or the disk. See
[full-disk encryption](/guides/operating-systems/full-disk-encryption/).

**End-to-end.** Only the endpoints can decrypt. This is a statement about _who holds
keys_, and it is stronger than transport encryption, where the server necessarily holds a
key. See
[end-to-end encrypted messaging](/guides/messaging/end-to-end-encrypted-messaging/).

## Four misconceptions

| Claim                                    | Reality                                                                               |
| ---------------------------------------- | ------------------------------------------------------------------------------------- |
| "Encrypted, so nobody can see it"        | Only the parties who hold a key. Metadata is unaffected.                              |
| "It's custom crypto, so it's stronger"   | Standard, reviewed primitives outperform novel ones almost every time.                |
| "A long key length makes it unbreakable" | Key length is rarely the constraint. Implementation and key management are.           |
| "No one has broken AES"                  | Nobody has needed to. Modern attacks target implementation, endpoints, and passwords. |

## Kerckhoffs's principle

> If an algorithm is assumed secret, it may be assumed insecure.

The security of a system must rest entirely on the secrecy of its keys, never on the
secrecy of its design. Every standard cryptographic primitive used today is public,
specified, and attacked in the open. That is the point.

:::tip
When someone proposes a proprietary encrypted product with no published design, the
absence of a specification is not a security feature. It means the security claim has
never been tested by anyone other than the author.
:::

## What actually breaks encryption

1. **The endpoint.** Malware running as you reads plaintext before encryption and after
   decryption. This is the most common failure by a wide margin.
2. **The key.** A key in a configuration file, in a repository, in a backup, or known to
   an adversary through legal process. See
   [key management](/guides/encryption/key-management/).
3. **The implementation.** Buffer handling, nonce reuse, padding oracles, and memory
   disclosure. [Heartbleed](/archive/security-incidents/heartbleed/) is a bounds-check bug
   with a CVSS score near perfect and enormous reach.
4. **The downgrade.** Old, weak protocol versions kept enabled for compatibility. A
   protocol that can be downgraded to a broken version is broken.

## Sources

- [RFC 8446](https://www.rfc-editor.org/rfc/rfc8446) — TLS 1.3, and the design decisions
  that removed downgrade and compression-related weaknesses.
- [NIST SP 800-57 Part 1 Rev. 5](https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final) — key
  management, the part that actually determines whether encryption helps.
- [NIST SP 800-38A](https://csrc.nist.gov/pubs/sp/800/38/a/final) — block cipher modes,
  and why the mode choice is not optional.
