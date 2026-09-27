---
title: 'DNS over HTTPS in Practice'
description: 'How DoH is deployed, why it was designed this way, and the operational details that decide whether it helps.'
category: 'dns'
difficulty: 'advanced'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['dns-over-https', 'dns', 'isps', 'protocol-design']
status: 'published'
sources:
  - title: 'RFC 8484: DNS Queries over HTTPS (DoH)'
    url: 'https://www.rfc-editor.org/rfc/rfc8484'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'DNS over HTTPS considerations for browsers'
    url: 'https://wiki.mozilla.org/Security/DOH-resolver-policy'
    publisher: 'Mozilla Foundation'
    kind: 'documentation'
    note: "Policy for Mozilla's Trusted Recursive Resolver (TRR) program, which is how Firefox resolves without deferring to the operating system resolver. The Mozilla support article of the same subject is only reachable through a bot challenge, so the wiki is cited instead."
    accessed: '2026-09-27'
  - title: 'Improving Privacy against Network Fingerprinting'
    url: 'https://www.rfc-editor.org/rfc/rfc7626'
    publisher: 'IETF'
    kind: 'standards'
    note: 'An earlier discussion of network-level privacy trade-offs.'
    accessed: '2026-09-27'
related:
  guides:
    ['dns/dns-privacy', 'browsers/browser-fingerprinting', 'network-privacy/home-network-privacy']
  archive: []
  news: []
---

DNS over HTTPS puts DNS queries inside HTTPS requests, using the same certificate
validation and the same ports as everything else on the web. The
[specification](https://www.rfc-editor.org/rfc/rfc8484) is short, and the interesting
decisions are all about the deployment model rather than the wire format.

## Why HTTPS and not a new protocol

The design decision that mattered was choosing to reuse HTTP infrastructure. The
alternative, a new protocol on a new port, faces the deployment problem described in
[RFC 7626](https://www.rfc-editor.org/rfc/rfc7626): anything on a new port is
identifiable and can be blocked or throttled as a class. Running inside ordinary HTTPS
means the traffic looks like web traffic, which is the entire point.

That is also the trade-off. A resolver that is a web endpoint inherits web's
centralisation, its caching, and its intermediaries.

## Query format

A DoH server accepts a GET or POST carrying a
[wire-format](https://www.rfc-editor.org/rfc/rfc1035) DNS message, and returns a response
in the same format with `application/dns-message`. Because HTTP already provides
connection reuse, compression, and transport security, most of the specification is about
caching and about which URL templates a client should use.

:::note
The important property is that a _browser_ can do DoH itself, rather than passing queries
to the operating system. The system resolver, the local network, and the ISP then see
neither the query nor which resolver was used — the browser opens the connection itself.
A client that delegates to the operating system does not get that property, which is why
"enable DoH in the router" is materially weaker than "enable DoH in the browser".
:::

## Deployment modes

**Browser-managed.** Firefox and Chrome resolve independently of the operating system
resolvers. This hides queries from the local network and the ISP, and exposes them to the
chosen resolver instead.

**Operating-system-managed.** The OS resolver wraps queries itself. Useful for devices
where the browser is not the main client, and for enforcing policy across applications.

**Router-managed.** Convenient and weak. The router resolves everything and the network
operator can see exactly what it asked for.

:::warning
"Opportunistic" mode tries encrypted DNS and falls back to plaintext if the secure
resolver is unreachable. In practice a hostile network can cause the failure and thereby
cause the downgrade, so the mode is only as good as the resolver's reachability. A strict
mode is what actually removes the fallback.
:::

## What a resolver can still do

- **See every query and every client address.** This is inherent. It is the party you have
  chosen to trust instead of your network.
- **Return a wrong answer.** DoH authenticates the resolver, not the answer. TLS gives no
  path to verifying that a resolver's response matches what the authoritative server
  would have said. DNSSEC is the mechanism that addresses this, and it has its own
  deployment gaps.
- **Correlate with the destination.** A resolver that also observes connections can
  reconstruct a browsing profile more easily than a network operator alone can.

:::tip
The privacy gain from DoH is real and worth taking. The additional step that makes it
durable is to use a resolver you have an actual relationship with — one you run, or one
whose business model does not depend on knowing what you look up.
:::

## Operational checklist

1. Browser-managed DoH, strict mode, no excluded domains.
2. A resolver whose retention policy you have read.
3. Confirm no fallback: [a leak test](https://www.dnsleaktest.com/) should show only your
   resolver.
4. Router DNS pointed at the local network rather than at a public resolver, so devices
   that are not the browser do not bypass it.
5. DNSSEC validation enabled if your resolver supports it, accepting that some domains
   will fail.
6. Re-test after every browser or operating-system update, because the defaults change.

## Sources

- [RFC 8484](https://www.rfc-editor.org/rfc/rfc8484) — the specification, including the
  media type and URL template conventions.
- [Mozilla: DNS over HTTPS design](https://wiki.mozilla.org/Security/DOH-resolver-policy) — why
  the browser resolves independently rather than using the system resolver.
- [RFC 7626](https://www.rfc-editor.org/rfc/rfc7626) — the network-fingerprinting problem
  that shaped both DoT and DoH.
