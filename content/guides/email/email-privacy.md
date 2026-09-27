---
title: 'Email Privacy'
description: 'Why email resists end-to-end encryption, and the specific compromises that are worth making.'
category: 'email'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['email', 'end-to-end-encryption', 'metadata', 'password-manager']
status: 'published'
sources:
  - title: 'RFC 5321: Simple Mail Transfer Protocol'
    url: 'https://www.rfc-editor.org/rfc/rfc5321'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'RFC 3207: SMTP Service Extension for Secure SMTP over TLS'
    url: 'https://www.rfc-editor.org/rfc/rfc3207'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Autocrypt Level 1'
    url: 'https://docs.autocrypt.org/level1.html'
    publisher: 'The Autocrypt Project'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'Surveillance Self-Defense: Why Communication Metadata Matters'
    url: 'https://ssd.eff.org/module/why-metadata-matters'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    note: 'The Surveillance Self-Defense collection has no email module; this is the module that covers the metadata argument made above.'
    accessed: '2026-09-27'
related:
  guides:
    [
      'messaging/end-to-end-encrypted-messaging',
      'password-managers/using-a-password-manager',
      'dns/dns-privacy',
    ]
  archive: []
  news: []
---

Email is the hardest common system to make private, and it is worth understanding why
before spending effort on it.

## The structural problem

Email was designed in 1981 to be a store-and-forward system that any server could relay a
message through. Every design decision since has preserved that property, because it is
what makes email work. The consequences:

- **Arbitrary servers handle plaintext.** Your message passes through your provider, your
  recipient's provider, and every intermediate relay, in the clear unless each hop
  happens to use TLS.
- **Transport security is opportunistic.** TLS between mail servers is not authenticated
  end to end in the general case, and a downgrade is not detectable by the user.
- **Metadata is the product.** Envelope data — who sent to whom, when, which servers were
  involved — is available to every hop and is the part attackers actually use.

:::note
This is why "end-to-end encrypted email" is a special request rather than a checkbox.
Ordinary SMTP gives the recipient's server the message in plaintext, so the server is by
construction able to read it. Any scheme that claims otherwise either encrypts to the
server as well, or changes the addressing model.
:::

## What is worth doing

**Use a provider you trust for at least one address.** This is the highest-value change,
because email is the account-recovery path for everything else you own. Migration to a
privacy-focused provider is a bigger job than configuring one, but it moves the most
consequential copy of your identity somewhere better.

**Turn on two-factor authentication and use an app-based code.** See
[two-factor authentication](/guides/authentication/two-factor-authentication/).

**Encrypt at rest where the provider supports it**, and understand that this protects you
from a stolen laptop or an insider with disk access, not from the provider.

**Send sensitive messages elsewhere.** For a document that must stay between two people,
use an encrypted file shared through a link with a password delivered out of band, or use
an end-to-end encrypted messenger. See
[end-to-end encrypted messaging](/guides/messaging/end-to-end-encrypted-messaging/).

:::warning
Do not rely on "S/MIME" or PGP on ordinary webmail. Both work, both are configured badly
by most people, and a key you never verified gives no protection against a substituted
key. Autocrypt exists to make opportunistic encryption safe by default rather than
requiring key management per correspondent.
:::

## Reducing metadata exposure

- Avoid putting anything sensitive in the **subject line**, which travels further than the
  body and is frequently logged separately.
- Understand that **the recipient list and the message ID are visible to every hop**. A
  `Message-ID` can carry a domain, a username, and a timestamp.
- Prefer services that do not retain message content after delivery, and check the
  retention policy rather than the marketing page.
- Remember **forwarding**. Once a message is forwarded, every previous hop's assumption
  about the recipient is void.

## A workable configuration

1. One account at a provider you have deliberately chosen; it becomes your recovery root.
2. Two-factor authentication with an authenticator app, plus a hardware key if your
   provider supports it.
3. Aliases per context if your provider supports them, so a breach of one address does not
   connect to the others.
4. Encrypted file transfer instead of attachment for anything that matters.
5. An [authenticated SPF](/guides/dns/dns-privacy/) and DKIM setup, so that your mail is
   harder to impersonate and harder to spam-filter out of other people's inboxes.

## Sources

- [RFC 5321](https://www.rfc-editor.org/rfc/rfc5321) — the SMTP specification, including
  the store-and-forward model that constrains everything.
- [RFC 3207](https://www.rfc-editor.org/rfc/rfc3207) — why plain SMTP has no
  authenticated transport.
- [Autocrypt Level 1](https://docs.autocrypt.org/level1.html) — a minimal, auditable standard
  for opportunistic encryption, designed so that key management is not the hard part.
