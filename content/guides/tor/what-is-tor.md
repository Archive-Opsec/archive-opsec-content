---
title: 'What Tor Is'
description: 'How onion routing works, what it guarantees, what it does not, and the misconceptions that cause harm.'
category: 'tor'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['tor', 'anonymity', 'encryption', 'onion-routing']
featured: true
status: 'published'
sources:
  - title: 'Tor Project: About Tor'
    url: 'https://www.torproject.org/about/'
    publisher: 'The Tor Project'
    kind: 'ngo'
    accessed: '2026-09-27'
  - title: 'Tor Metrics'
    url: 'https://metrics.torproject.org/'
    publisher: 'The Tor Project'
    kind: 'ngo'
    note: 'The authoritative source for relay and network counts, rather than a rounded figure quoted elsewhere.'
    accessed: '2026-09-27'
  - title: 'Tor: The Second-Generation Onion Router'
    url: 'https://svn-archive.torproject.org/svn/projects/design-paper/tor-design.html'
    publisher: 'The Tor Project'
    kind: 'documentation'
    note: 'The separately titled "Tor Relay System" page cited previously is not present in the Tor Project design-paper archive index; this is the design paper by the same authors, and the one that sets out circuit construction and the first, middle and last relay roles. It predates the "guard" terminology, so it says "entry" where current Tor documentation says "guard".'
    accessed: '2026-09-27'
  - title: 'How HTTPS and Tor Work Together to Protect Your Anonymity and Privacy'
    url: 'https://tor-https.eff.org/'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    note: 'The Surveillance Self-Defense module "Tor and HTTPS" was moved off ssd.eff.org onto this standalone EFF microsite. It still resolves from https://www.eff.org/pages/tor-and-https, and the current SSD guide "How to - Use Tor" links to it as further reading.'
    accessed: '2026-09-27'
related:
  guides:
    [
      'tor/tor-browser-and-search',
      'vpn/what-vpns-do-and-dont',
      'metadata/metadata-explained',
      'browsers/browser-fingerprinting',
    ]
  archive: []
  news: []
---

Tor routes traffic through a volunteer-run network of relays so that no single party can
see both who is connecting and what they are connecting to. That is a narrower and more
specific claim than most descriptions of it, and understanding the difference is the point
of this page.

## How a circuit is built

1. Your client asks a **guard relay**, which is a relay it has agreed to use for a period
   of time. The guard learns your IP address. Nothing else does.
2. The guard contacts a **middle relay**, which learns the guard but not your address.
3. The middle contacts an **exit relay**, which completes the connection. Only the exit
   sees your destination, and only if you have not also used an onion service.
4. The reply travels back along the same path.

Traffic between the relays is layered — "onion" — so that each relay knows only its own
neighbour in either direction. The circuit is normally rebuilt every few minutes, so no
single relay observes more than a small amount of your traffic.

:::note
The design does not hide _that_ you are using Tor from your network. It hides what you
visit, from everyone along the path, and hides the two ends from each other. A network
administrator who wants to know that a machine is on the Tor network can usually find
that out, and historically many deliberately do.
:::

## What Tor protects against

- **Local network monitoring.** A café or workplace network sees an encrypted connection
  to a relay, not the destination.
- **Service providers.** The destination sees a connection from an exit relay.
- **Passive network observers** who cannot see inside the circuit.
- **Tracking and fingerprinting** when using Tor Browser, which standardises the
  fingerprint so you are indistinguishable from other users.

## What Tor does not protect against

:::warning

- **A global adversary that controls or observes a large fraction of the network.** Both
  ends of a circuit are known to a sufficiently well-placed observer. Tor raises cost
  and reduces casual exposure; it does not defeat an adversary that can watch most of the
  internet.
- **A malicious exit.** An exit relay can observe plaintext HTTP traffic and alter it. TLS
  certificate validation is what prevents this, which is why the browser refuses
  certificate warnings rather than letting you click through.
- **A compromised endpoint.** Malware with your privileges reads your traffic before
  encryption. See [browser fingerprinting](/guides/browsers/browser-fingerprinting/).
- **Your own behaviour.** Logging in to an account identifies you, regardless of the
  transport. Two Tor users with identical writing styles and reading habits are also
  correlatable.
- **Being a very large share of the network.** See [Tor Metrics](https://metrics.torproject.org/)
  for actual relay counts rather than a figure remembered from a blog post.
  :::

## Onion services

An `.onion` address resolves within the network, so there is no exit relay and no DNS
lookup. The service learns the client's exit from the rendezvous point, not from a
connection to a known address, and users authenticate to the service with a client
certificate. This is a meaningfully stronger design than a web page reached through a
circuit.

## Common misconceptions

| Claim                                    | Reality                                                                                                                                             |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Tor is slow because it is weak"         | Circuits, and guard and exit relay capacity relative to user count. See metrics.                                                                    |
| "Tor is anonymous, full stop"            | It hides your network location and destination from each other. Accounts and behaviour still identify you.                                          |
| "The Tor Project can read messages"      | It cannot, and cannot be compelled to. The [Double Ratchet](/guides/messaging/end-to-end-encrypted-messaging/) design has no server-side plaintext. |
| "A VPN plus Tor is automatically better" | It depends entirely on who you were trying to hide from. See [what VPNs do and do not](/guides/vpn/what-vpns-do-and-dont/).                         |
| "There is a backdoor"                    | No such claim should be repeated without a document. Anyone asserting one should be asked for the primary source.                                   |

## Sources

- [About Tor](https://www.torproject.org/about/) — the protocol as its designers
  describe it.
- [Tor Metrics](https://metrics.torproject.org/) — current, verifiable network figures.
- [Tor: The Second-Generation Onion Router](https://svn-archive.torproject.org/svn/projects/design-paper/tor-design.html)
  — the design paper's account of entry, middle and exit roles. (The paper predates the
  "guard" terminology and uses "entry".)
- [EFF: Tor and HTTPS](https://tor-https.eff.org/) — why the two are
  complementary rather than substitutes.
