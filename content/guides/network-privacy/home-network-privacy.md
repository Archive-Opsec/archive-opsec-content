---
title: 'Home Network Privacy'
description: 'Your router sees everything, and the devices on your network can see each other. Both are worth fixing.'
category: 'network-privacy'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['isps', 'dns', 'self-hosting', 'metadata', 'hardening']
status: 'published'
sources:
  - title: 'RFC 1918: Address Allocation for Private Internets'
    url: 'https://www.rfc-editor.org/rfc/rfc1918'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'NIST SP 800-193: Platform Firmware Resiliency Guidelines'
    url: 'https://csrc.nist.gov/pubs/sp/800/193/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-17'
  - title: 'Consumer Guidance: Home Network Security'
    url: 'https://www.ncsc.gov.uk/section/information-for/individuals-families'
    publisher: 'UK National Cyber Security Centre'
    kind: 'government'
    accessed: '2026-09-27'
related:
  guides:
    [
      'dns/dns-privacy',
      'vpn/what-vpns-do-and-dont',
      'operating-systems/hardening-basics',
      'browsers/choosing-a-browser',
    ]
  archive: []
  news: []
---

Most threat modelling starts with the internet. The network inside your house sees more,
and is easier to fix.

## What the router sees

Every device's traffic, every DNS lookup, every device that connects, and when. Many
routers keep connection logs, some indefinitely, and the default is usually "record
everything".

## What the devices see of each other

On a typical home network, every device can reach every other device directly. That means
a compromised smart bulb, a television, or a printer can reach your laptop, your NAS, and
your phone — and a service that simply queries the local network gets a response.

:::note
Protocols that make this visible are designed to make local devices findable. mDNS and
SSDP announce services by name across the subnet. A malicious or compromised site in a
browser cannot always reach them directly, but a malicious _device_ on your network has no
such restriction.
:::

## Changes, in order of value

1. **Update the router firmware**, and check whether it is still supported. Routers are
   the least updated device in most homes.
2. **Change the administrative credentials**, and disable remote administration unless you
   need it.
3. **Use WPA2 or WPA3 with a long passphrase.** A router still using WEP, or a short
   administrative password that is also the Wi-Fi key, is the most common home network
   problem.
4. **Turn off UPnP** unless you have a specific need for it. UPnP lets a device on your
   network ask the router to open a port to the internet.
5. **Segment**: put untrusted and smart devices on a guest network, and keep the
   workstation, the phone, and anything holding credentials on the main one. Guest
   networks exist for this and are almost always unused.
6. **Point the router's DNS at a resolver you control**, so devices that ignore your
   browser still do not leak to your ISP. See [DNS privacy](/guides/dns/dns-privacy/).
7. **Reduce logging**, and check what the router retains.
8. **Audit what is connected.** A device list you have never reconciled is the usual way
   unknown hardware joins a network.

```text
router.local  — administrative interface: restrict by source, or bind to the LAN only
192.168.1.1   — the most common default; check whether yours is remotely reachable
```

:::warning
Firmware versions for routers are the least visible security state in a home. Check the
vendor's support list, not the router's own settings page, which often reports a version
that is several years old with no indication that it matters.
:::

## IPv6 and RA

IPv6 changes the threat model in a way people miss: devices have globally routable
addresses by default, and neighbour discovery is how they find each other. If you disable
IPv6, understand that some things break; if you keep it, the segmentation above matters
more, not less. Router advertisement settings belong in the same review as the Wi-Fi
settings.

## What this does not solve

- Your ISP still sees your traffic to the internet. This is about the local segment.
- Devices with a microphone and a network radio can exfiltrate on their own schedule.
- Physical access to your router gives access to everything on it. This is a home, not a
  data centre.
- A device that is already compromised on your network is not fixed by segmentation
  alone, though segmentation limits what it can reach.

:::tip
If you only do two things: update the router, and move the smart devices and the guest
computers to a guest network. Those two changes close the paths that actually get used.
:::

## Sources

- [RFC 1918](https://www.rfc-editor.org/rfc/rfc1918) — why private address ranges say
  nothing about exposure, and are frequently misused as a security boundary.
- [NIST SP 800-193](https://csrc.nist.gov/pubs/sp/800/193/final) — platform firmware
  protection, relevant to the router and to any device you install firmware onto.
- [UK NCSC: Information for individuals and families](https://www.ncsc.gov.uk/section/information-for/individuals-families)
  — practical home network guidance from a national CERT.
