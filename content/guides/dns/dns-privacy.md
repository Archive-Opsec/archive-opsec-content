---
title: 'DNS Privacy'
description: 'Why name resolution is the most useful thing your network can see, and what encrypted DNS changes.'
category: 'dns'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['dns', 'dns-over-https', 'dns-over-tls', 'isps', 'metadata']
status: 'published'
sources:
  - title: 'RFC 8484: DNS Queries over HTTPS (DoH)'
    url: 'https://www.rfc-editor.org/rfc/rfc8484'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'RFC 7858: DNS over Transport Layer Security (DoT)'
    url: 'https://www.rfc-editor.org/rfc/rfc7858'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'RFC 1035: Domain Names — Implementation and Specification'
    url: 'https://www.rfc-editor.org/rfc/rfc1035'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Encrypted DNS in Firefox'
    url: 'https://support.mozilla.org/en-US/kb/dns-over-https'
    publisher: 'Mozilla Foundation'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides:
    ['dns/dns-over-https', 'network-privacy/home-network-privacy', 'vpn/what-vpns-do-and-dont']
  archive: []
  news: []
---

When you visit a site, your device must first turn a name into an address. That lookup is
plaintext by default, and it happens before any encryption to the site can begin. It is
therefore the most reliable thing a network can observe about you, for free.

## What DNS reveals

A resolver sees the name you asked for and where the request came from. A network
operator sees the same thing, plus timing, and plus the IP address you then connect to.
Together, name lookups and connections describe your browsing in detail without any
content being read.

:::note
DNS predates HTTPS and was designed for a network of cooperating hosts, so it has no
integrity or confidentiality mechanism. This is in
[RFC 1035](https://www.rfc-editor.org/rfc/rfc1035) itself: resolution was assumed to be
either trusted or irrelevant, and a decade of third-party resolvers turned that
assumption into a permanent exposure.
:::

## What encrypted DNS changes

**DNS over TLS** ([RFC 7858](https://www.rfc-editor.org/rfc/rfc7858)) and **DNS over
HTTPS** ([RFC 8484](https://www.rfc-editor.org/rfc/rfc8484)) wrap resolution in a
transport the resolver must authenticate. The local network and the ISP then see only that
a connection to a named resolver exists.

This is a real and worthwhile improvement. It is also frequently oversold:

:::warning

- **The resolver still sees every query.** You have moved the observation from your ISP to
  a third party. If the resolver is run by an advertising business, the record is now
  available to that business and not to your network.
- **It is not end-to-end.** Resolution is not encrypted all the way to the authoritative
  server, so a resolver can still lie about an answer. TLS authenticates the resolver,
  it does not make the response verifiable.
- **It does not hide the rest.** If you use DoH and then make a plaintext HTTP request, or
  connect to a service without TLS, the network learns the destination directly and the
  DNS protection is beside the point.
- **It can be blocked or ignored**, and a device that falls back to plaintext DNS without
  telling you has worse privacy than one that never offered encryption.
  :::

## Choosing a resolver

| Option                                | Trust model                 | Notes                                               |
| ------------------------------------- | --------------------------- | --------------------------------------------------- |
| Your ISP's resolver                   | ISP sees everything         | The default; no configuration needed                |
| A browser-embedded resolver           | Browser vendor sees queries | Firefox's DoH is a direct-to-resolver design        |
| An independent resolver you pay for   | The operator sees queries   | Read the retention policy                           |
| A local caching resolver              | Only you                    | dnsmasq, unbound, CoreDNS; still needs an upstream  |
| A resolver in your own infrastructure | Only you                    | For the technically confident, the strongest option |

:::tip
If you can run one, a local caching resolver forwarding to a DoT or DoH upstream gives you
the privacy benefit while keeping the dependency list short. `unbound` and `dnsmasq` are
the usual choices.
:::

## Configuring it

In Firefox, which ships with its own resolver rather than using the system one:

```text
// about:config
network.trr.mode                          = 3   # 3 = DoH only, 2 = opportunistic
network.trr.uri                           = "https://dns.example/dns-query"
network.trr.custom_uri                    = false
network.trr.excluded-domains             = ""   # no fallbacks
network.trr.strict_native_fallback        = true
```

In Chrome, the setting is _Secure DNS_, and it offers a choice of provider — read the list
before selecting, since it is a list of companies gaining visibility into your lookups.

On a Linux host with `systemd-resolved`, unencrypted DNS should be routed to the local
stub listener rather than used directly:

```ini
# /etc/systemd/resolved.conf
[Resolve]
DNS=1.1.1.1
FallbackDNS=
DNSOverTLS=yes
DNSSEC=allow-downgrade
```

:::warning
Setting `FallbackDNS=` empty is the part people miss. With a fallback configured,
encrypted DNS is opportunistic: if the secure resolver fails, resolution silently
reverts to plaintext and nothing tells you.
:::

## Verifying

- [DNS leak tests](https://www.dnsleaktest.com/) show which resolvers observed a lookup.
  A correctly configured client should show only the resolver you chose.
- Query the special names your resolver provides to report its own identity, if it has
  them.
- Watch the connection in a packet capture on a trusted network, not in production.

## Sources

- [RFC 8484](https://www.rfc-editor.org/rfc/rfc8484) — DNS over HTTPS, including the
  threat model it addresses and the residual exposure it acknowledges.
- [RFC 7858](https://www.rfc-editor.org/rfc/rfc7858) — DNS over TLS, and why port 853
  and certificate validation are part of the design.
- [RFC 1035](https://www.rfc-editor.org/rfc/rfc1035) — the original specification, with no
  security considerations to speak of.
- [Firefox DNS over HTTPS](https://support.mozilla.org/en-US/kb/dns-over-https) — the
  current settings and what each `network.trr.mode` value means.
