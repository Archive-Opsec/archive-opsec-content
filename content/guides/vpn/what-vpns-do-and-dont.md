---
title: 'What VPNs Do and Do Not Do'
description: 'The single change a VPN makes, the trust it transfers rather than removes, and how to read a provider claim.'
category: 'vpn'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['vpn', 'isps', 'encryption', 'trust']
featured: true
status: 'published'
sources:
  - title: 'RFC 7457: Summarizing Known Attacks on VPNs'
    url: 'https://www.rfc-editor.org/rfc/rfc7457'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Mullvad VPN: Policies'
    url: 'https://mullvad.net/en/policies'
    publisher: 'Mullvad VPN'
    kind: 'company'
    note: 'Replaces the retired /en/help/policy page. This is the current index of Mullvad policy documents; the specific no-logging commitment is at https://mullvad.net/en/help/no-logging-data-policy'
    accessed: '2026-09-27'
  - title: 'Does Proton VPN keep logs?'
    url: 'https://protonvpn.com/support/no-logs-vpn'
    publisher: 'Proton AG'
    kind: 'company'
    note: 'A source claim by the operator, not independent evidence. The same no-logs claim has been independently audited by Securitum; Proton write-up of that audit: https://protonvpn.com/blog/no-logs-audit/'
    accessed: '2026-09-27'
  - title: 'IVPN Policy'
    url: 'https://www.ivpn.net/en/privacy/'
    publisher: 'IVPN'
    kind: 'company'
    accessed: '2026-09-27'
related:
  guides:
    [
      'tor/what-is-tor',
      'dns/dns-privacy',
      'network-privacy/home-network-privacy',
      'encryption/encryption-explained',
    ]
  archive: []
  news: []
---

A VPN replaces one trusted network with another trusted network. That is the whole idea,
and it is useful — but it is a transfer of trust, not a removal of it, and the
distinctions matter more than the product comparison.

## What it changes

Your network — a café router, a hotel, an employer, an ISP — no longer sees the
destinations you connect to. It sees an encrypted connection to a VPN operator's server.
The destination sees the VPN operator's address instead of yours, and may apply its own
geography-based access rules as a result.

The connection is encrypted in transit between you and the operator. Nothing about the
content changes: a request to an `http://` site is still plaintext to whatever handles
it next.

## What it does not change

:::warning

- **It does not make you anonymous.** The operator knows your real IP address and your
  destination. A single operator is a single point of observation.
- **It does not fix fingerprinting.** Your browser is still your browser. See
  [browser fingerprinting](/guides/browsers/browser-fingerprinting/).
- **It does not fix malware, phishing, or account compromise.** It has no effect on a
  malicious page or a reused password.
- **It does not hide the websites you use from each other**, and it does not stop
  behavioural profiling by the destination.
- **It does not protect traffic you send outside the tunnel.** Anything that bypasses the
  tunnel — a misconfigured route, a system service — is exposed again.
- **It does not stop the destination from logging.** Many services log by policy
  regardless of the apparent client address.
  :::

## The leak paths that matter in practice

**DNS.** If name resolution still goes to your ISP, the ISP learns the sites you visit
even while the tunnel is running. This is the most common real-world gap, and it is why
[encrypted DNS](/guides/dns/dns-privacy/) matters alongside a VPN rather than instead of
it. Some clients offer to route DNS through the tunnel; check rather than assume.

**IPv6 and WebRTC.** A tunnel over IPv4 that leaves IPv6 traffic outside the tunnel is a
complete bypass. This is a configuration bug rather than a design limitation, and it has
been found in real products.

**Kill switches.** A "killswitch" blocks traffic when the tunnel drops. Without one, a
failed connection silently reverts to the unprotected path.

:::note
The failure mode to design for is the tunnel dropping silently. If your threat model
includes a hostile network, an always-on kill switch is part of the product requirement,
not an optional extra.
:::

## Reading a provider claim

The verifiable properties, in rough order of usefulness:

1. **A named entity and jurisdiction.** Anonymity requires that some operator can be
   compelled and has nothing to hand over. A company with no registered entity, or one in
   a jurisdiction with no applicable law, is a different proposition.
2. **A specific logging policy.** What is logged, and for how long. "No logs" without
   saying _what_ is not a policy.
3. **Independent audit.** A published third-party audit of the no-logs claim is
   materially stronger than a policy page. Read the scope of the audit, not just its
   existence.
4. **Transparency reporting.** How many times the operator has been asked for data and
   what it produced.
5. **Payment without an account.** Paying with an account-linked method creates a record
   that links you to a subscription.
6. **Published technical detail.** Protocol, key exchange, DNS handling, and IPv6
   behaviour.

:::warning
"No logs" is a claim by the party you are asking to trust. Treat the audit and the
jurisdiction as the evidence, and the policy page as a summary of it.
:::

## When not to bother

- You mostly need a second factor and unique passwords.
- Your threat is malware or phishing.
- You are on a network you control and trust.
- You need to log into services that block VPNs, and the only way through is a shared
  address that many people also use.

If your goal is not to be identifiable at all, use
[Tor](/guides/tor/what-is-tor/). If the goal is to stop a café or an employer from reading
the sites you visit, a correctly configured VPN is a reasonable, cheap control.

## Sources

- [RFC 7457](https://www.rfc-editor.org/rfc/rfc7457) — an IETF document cataloguing
  attacks on VPN deployments, including the ones above. Not a marketing document.
- [Mullvad policy](https://mullvad.net/en/policies), [Proton VPN
  no-logs](https://protonvpn.com/support/no-logs-vpn) and [IVPN
  policy](https://www.ivpn.net/en/privacy/) — read as source claims from three
  providers that publish specific policies, and compare what each commits to.
