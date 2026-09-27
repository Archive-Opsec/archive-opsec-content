---
title: 'End-to-End Encrypted Messaging'
description: 'What the encryption protects, what the provider still sees, and why metadata is usually the real story.'
category: 'messaging'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['end-to-end-encryption', 'messaging', 'metadata', 'key-management']
featured: true
status: 'published'
sources:
  - title: 'The Double Ratchet Algorithm'
    url: 'https://signal.org/docs/specifications/doubleratchet/'
    publisher: 'Signal'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'X3DH Key Agreement'
    url: 'https://signal.org/docs/specifications/x3dh/'
    publisher: 'Signal'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'RFC 8446: The Transport Layer Security (TLS) Protocol Version 1.3'
    url: 'https://www.rfc-editor.org/rfc/rfc8446'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Sealed Sender'
    url: 'https://signal.org/blog/sealed-sender/'
    publisher: 'Signal'
    kind: 'company'
    accessed: '2026-09-27'
related:
  guides: ['encryption/encryption-explained', 'metadata/metadata-explained', 'email/email-privacy']
  archive: []
  news: []
---

End-to-end encryption means the message is encrypted by the sender and decrypted by the
recipient, and nobody in between — including the service operator — holds a key that can
read it. Everything worth knowing about secure messaging is downstream of that fact.

## What the operator can and cannot see

With properly implemented end-to-end encryption, the operator cannot read message
contents. It can still see, in most designs:

- **Who is talking to whom.** The account graph, present in plaintext or trivially
  derivable, is often the most valuable part of the dataset.
- **When.** Message timestamps, and how long sessions last.
- **How much.** Byte counts per conversation, per hour.
- **With what.** Client versions, IP addresses, device identifiers, and account recovery
  details.

This is not a defect in the encryption. It is a property of routing: any system that
delivers a message to a device must know enough to deliver it. The tools that reduce
metadata reduce it by adding cost or friction — padding message sizes, batching delivery,
or routing through a relay that hides the sender.

## What good implementations do

**Key agreement.** X3DH lets a message be encrypted to a recipient's key even when the
recipient is offline, using pre-published pre-keys. See the
[X3DH specification](https://signal.org/docs/specifications/x3dh/).

**Forward and post-compromise secrecy.** The
[Double Ratchet](https://signal.org/docs/specifications/doubleratchet/) updates the
encryption key after every message, so a stolen key does not decrypt earlier
traffic and a restored session does not silently return to an old key.

**Identity verification.** Safety numbers let two people confirm out of band that no
server substituted a key. Verification matters more than the protocol: an encrypted
channel to an attacker-controlled key is still encrypted.

:::warning
Group chats, channels, and any feature involving a server-side copy reintroduce the
provider as a participant. Ask specifically whether a given feature is end-to-end
encrypted, and what happens to a conversation when a member leaves.
:::

## Choosing a service

The honest comparison is not "which is most private" but "what is each one structurally
able to do".

| Property                              | Why it matters                                                  |
| ------------------------------------- | --------------------------------------------------------------- |
| Published protocol and implementation | A claim you can check against a specification and source        |
| Open source client                    | The part that touches your keys should be auditable             |
| Audited implementation                | Cryptography that has not been reviewed is a hypothesis         |
| No phone-number requirement           | Removes the SIM as an identity anchor                           |
| Encrypted backups                     | Backups are the usual place a chat history ends up readable     |
| No message history for new devices    | Avoids a silent second copy                                     |
| Metadata minimisation                 | Sealed sender, private contact discovery, disappearing messages |

:::note
End-to-end encryption is a property of a design, not a feature. It can be added to a
service that has already collected the metadata, and removed again. Prefer services that
have been end-to-end by design for years over one that added it recently, and check
whether the _backups_ are covered.
:::

## Practical advice

1. Use one service for sensitive conversations and another for everything else.
2. Verify keys in person for conversations where an active attack is plausible.
3. Turn on disappearing messages where the retention policy allows, remembering that
   recipients can still photograph a screen.
4. Assume the _service_ is honest and the _device_ is not compromised. An attacker with
   read access to your unlocked phone defeats any protocol.
5. Do not send one-time secrets or passwords through a chat, even an encrypted one.

## Sources

- [Signal X3DH specification](https://signal.org/docs/specifications/x3dh/) — how a
  message is encrypted to an offline recipient.
- [Signal Double Ratchet specification](https://signal.org/docs/specifications/doubleratchet/)
  — the key-update mechanism behind forward secrecy.
- [Signal on Sealed Sender](https://signal.org/blog/sealed-sender/) — a concrete
  example of removing the sender field from the operator's view.
- [RFC 8446](https://www.rfc-editor.org/rfc/rfc8446) — TLS 1.3, which protects the
  transport to the server but says nothing about content.
