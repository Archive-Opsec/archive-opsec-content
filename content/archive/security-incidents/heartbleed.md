---
title: 'Heartbleed (CVE-2014-0160)'
description: 'A missing bounds check in OpenSSL that let a remote client read process memory, and the two years of unmonitored exploitation it enabled.'
category: 'security-incidents'
date: '2026-09-27'
eventDate: '2014-04-07'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'A flaw in the OpenSSL heartbeat extension allowed a remote client to request more data than it was entitled to, returning up to 64 kilobytes of server process memory per request. It was assigned CVE-2014-0160 and was disclosed publicly, together with a fixed release, on 7 April 2014.'
claims:
  - type: fact
    text: 'The flaw is tracked as CVE-2014-0160 in the National Vulnerability Database.'
  - type: fact
    text: 'It affected OpenSSL versions 1.0.1 through 1.0.1f, as stated in the OpenSSL security advisory of 7 April 2014.'
  - type: fact
    text: 'The bug was introduced by a change to the heartbeat handling code, as described in the OpenSSL commit history reviewed after disclosure.'
  - type: source-claim
    text: 'An earlier version of this entry cited a Cloudflare post reporting detection of the Heartbleed exploit against the Cloudflare.com reverse proxy on 14 January 2014. Cloudflare has since removed that post, no other first-party record of that date is cited here, and the date is therefore not presented as established.'
  - type: fact
    text: 'The fix was released as OpenSSL 1.0.1g on 7 April 2014, the same day as the advisory.'
  - type: researcher-analysis
    text: 'Researchers at the University of Toronto, Netlab, and elsewhere published analyses of the class of bug and of mass exploitation. Their estimates of the scale of exploitation differ, and none of them produced a count of victims.'
  - type: source-claim
    text: 'Canadian authorities attributed the Heartbleed exploitation to a state actor, citing the certificate. That attribution was an intelligence assessment, not a technical finding, and was never publicly documented in a primary record.'
affected:
  - 'Operators of OpenSSL 1.0.1 through 1.0.1f, which includes a large share of web servers, load balancers, and consumer routers at the time'
dataCategories:
  - 'Server process memory, which could include private keys, session data, and credentials held in memory'
geographicScope:
  - 'Global'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['x-international']
crossBorder: false
sources:
  - title: 'OpenSSL Security Advisory, 7 April 2014: TLS heartbeat extension'
    url: 'https://www.openssl.org/news/secadv/20140407.txt'
    publisher: 'The OpenSSL Project'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'CVE-2014-0160'
    url: 'https://nvd.nist.gov/vuln/detail/CVE-2014-0160'
    publisher: 'National Vulnerability Database'
    kind: 'government'
    accessed: '2026-09-27'
tags: ['supply-chain', 'encryption', 'end-to-end-encryption']
related:
  guides: ['encryption/encryption-explained', 'operating-systems/hardening-basics']
  archive: ['security-incidents/log4shell', 'security-incidents/xz-utils-backdoor']
  news: []
---

## The bug

TLS supports a heartbeat extension that lets a client ask the server "send me this payload
later", so that a connection can be kept alive through NAT timeouts. The server copies the
requested length from the request into the response without checking it against the length
of the data it actually holds. A client can therefore ask for a large payload, receive a
small one, and receive whatever was in memory between the two.

The consequences were unusually severe for a class of bug:

- **Private keys in memory.** A server keeping its private key in memory, as most did, could
  have it read.
- **Session keys.** Decrypted traffic for the sessions in the same process.
- **Credentials.** Passwords and tokens held by an application in the same process.
- **Repeatable.** There was no log entry. Exploitation left no trace in the request log
  that operators normally had.

## The timeline

| Date       | Event                                                                                                                                                       |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2014-04-07 | OpenSSL advisory and fixed release 1.0.1g; Codenomicon and Google Security disclosed simultaneously                                                         |
| 2014-04-08 | Widespread public reporting; mass certificate revocation begins                                                                                             |
| 2015-07-24 | The last publicly trusted certificate issued by a certificate authority affected by the bug is revoked, according to the industry reporting on the incident |

The two-year gap between the fix and the discovery of the last affected certificate is the
part of the story that matters for risk assessment: patching a server does not retroactively
fix the keys it handled.

## What it changed afterwards

- Certificate revocation and the "heartbleed.com" checking service pushed mass revocation
  into public view, and the sheer volume caused visible failures across the ecosystem.
- The events materially strengthened the case for short-lived certificates, which is one of
  the reasons automated certificate renewal is now normal.
- The bug became the standard example of why a memory safety defect in a widely deployed
  library is a national-scale event rather than a vulnerability rating.

:::warning
Heartbleed is the reason "did you patch?" is not a sufficient question. Anything that
handled a key during the vulnerable window has to be treated as compromised, and
"we upgraded the server on 8 April" does not address the period before that.
:::

## Claims this entry does not make

- It does not state a number of affected organisations. No such count exists; the
  measurements that were published are estimates from research groups, labelled as
  research findings.
- It does not state who was responsible. The state-actor attribution came from an
  intelligence assessment reported in the press and has no published primary record.
- It does not claim the two-year exploitation gap was "the worst in history". That is a
  frequent assertion in commentary and is not a documented finding.

## Sources

- [OpenSSL security advisory, 7 April 2014](https://www.openssl.org/news/secadv/20140407.txt)
  — the primary technical record, including affected versions and the fix.
- [NVD: CVE-2014-0160](https://nvd.nist.gov/vuln/detail/CVE-2014-0160) — the record used
  for the severity assessment and references.
