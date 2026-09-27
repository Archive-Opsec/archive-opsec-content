---
title: 'Metadata Explained'
description: 'A worked primer on data about data: what leaks even with perfect encryption, and the measures that actually reduce it.'
category: 'metadata'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['metadata', 'anonymity', 'end-to-end-encryption', 'digital-footprint']
featured: true
status: 'published'
sources:
  - title: 'Metadata Equals Surveillance'
    url: 'https://www.schneier.com/blog/archives/2013/09/metadata_equals.html'
    publisher: 'Schneier on Security'
    kind: 'ngo'
    note: 'Posted 23 September 2013, not January 2015. Replaces a 2015-dated URL whose title matched no Schneier post; the old path now redirects to this article.'
    accessed: '2026-09-27'
  - title: 'Robust De-anonymization of Large Sparse Datasets'
    url: 'https://doi.org/10.1109/SP.2008.33'
    publisher: 'IEEE Symposium on Security and Privacy'
    kind: 'academic'
    note: 'Narayanan and Shmatikov, 2008 — re-identification from a supposedly de-identified dataset.'
    accessed: '2026-09-27'
  - title: 'Unique in the Crowd: The privacy bounds of human mobility'
    url: 'https://doi.org/10.1038/srep01359'
    publisher: 'Scientific Reports'
    kind: 'academic'
    note: 'de Montjoye et al., 2013.'
    accessed: '2026-09-27'
  - title: 'RFC 8446: TLS 1.3'
    url: 'https://www.rfc-editor.org/rfc/rfc8446'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
related:
  guides:
    [
      'messaging/end-to-end-encrypted-messaging',
      'tor/what-is-tor',
      'dns/dns-privacy',
      'encryption/encryption-explained',
    ]
  archive: []
  news: []
---

Metadata is data about data. It is what a system knows because you used it, rather than
because of what you said. The reason it matters is that the content is often protected
and the metadata is not.

## A worked example

Consider an end-to-end encrypted message from Alice to Bob. The operator cannot read it.
It can still see:

- Alice's and Bob's account identifiers
- the time, to the second
- the message size
- the IP address each device connected from
- the client software version
- how long the session lasted, and how many messages followed

None of that is the message. Together, it is a very good description of a relationship and
its timing. Add a movement history, and you have a location; add a
[de-anonymisation result](/archive/), and you have a name.

:::note
[Narayanan and Shmatikov](https://doi.org/10.1109/SP.2008.33) demonstrated
re-identification of a de-identified movie-rating dataset, and
[de Montjoye et al.](https://doi.org/10.1038/srep01359) found that a handful of
location points identify most individuals. Both were published results on data that was
supposedly anonymous. The pattern is general: "anonymous" data usually is not.
:::

## The five leaks that recur

**Timing.** Who talked to whom and when. Often more identifying than content. It is the
reason Tor rebuilds circuits and why some protocols pad message sizes.

**Volume.** How much data, in what pattern. Download patterns identify content; a large
transfer at a specific time is a strong signal.

**Network location.** IP addresses, and the radio-level identifiers devices broadcast.
Resolved roughly by anyone with a database.

**Device identity.** Advertised identifiers, fingerprintable configuration, and
[hardware serial numbers](https://support.apple.com/guide/security/secure-software-updates-sec5599b66df/web).

**Retention and linkage.** The same identifier used across contexts, for years, is what
turns many small records into one profile.

## What reduces metadata

| Measure                       | Reduces                           | Cost                                 |
| ----------------------------- | --------------------------------- | ------------------------------------ |
| Traffic padding               | Size and pattern leakage          | Bandwidth, latency                   |
| Batched or delayed delivery   | Timing leakage                    | Delay                                |
| Message batching              | Timing and size                   | Delay, complexity                    |
| Metadata-minimising protocols | Server-side records               | Requires protocol change             |
| Anonymous addressing          | Linkability                       | Usability, a directory may be needed |
| Relay or mix networks         | Linkability to the client         | Latency, the reason for Tor          |
| Encrypted DNS                 | Name lookups on the local network | Trust in the resolver                |
| Short retention periods       | Everything, eventually            | Operational work for the holder      |

:::warning
None of these are optional add-ons to encryption. A protocol that encrypts content and
leaves precise timing in the clear has moved the problem, not solved it. Conversely, a
protocol that minimises metadata while transmitting content in the clear has failed
entirely.
:::

## Reading a claim about metadata

When someone says a system is private, ask:

1. Does the service learn who communicated with whom?
2. Does it learn when, and how often?
3. Does it learn the sizes?
4. Is there a mechanism to say _no_ to content collection while the system still works?
5. What is retained after deletion is requested, and who can be made to produce it?

A system that answers all five is worth trusting more than one that answers only the
first, and considerably more than one that answers none of them.

## Sources

- [Schneier: Metadata Equals Surveillance](https://www.schneier.com/blog/archives/2013/09/metadata_equals.html) — a
  short, quotable argument that collecting metadata is surveillance rather than a lesser
  form of it, written in 2013. Useful for the framing, not for a technical taxonomy of
  what metadata reveals.
- [Narayanan & Shmatikov](https://doi.org/10.1109/SP.2008.33) — _IEEE S&P_ 2008.
- [de Montjoye et al.](https://doi.org/10.1038/srep01359) — _Scientific Reports_ 3, 2013.
