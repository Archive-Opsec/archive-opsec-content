---
title: 'Public Wi-Fi and hostile networks'
description: 'What a public network can observe, what HTTPS protects, and how to reduce exposure when the network itself is not trustworthy.'
category: 'network-privacy'
updated: '2026-09-27'
added: '2026-09-27'
author: 'Archive-Opsec contributors'
contributors: []
difficulty: 'introductory'
tags: ['network-privacy', 'wi-fi', 'vpn', 'https', 'threat-model']
featured: false
status: 'published'
sources:
  - title: 'The Transport Layer Security Protocol Version 1.3'
    url: 'https://www.rfc-editor.org/rfc/rfc8446'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Wi-Fi security guidance'
    url: 'https://consumer.ftc.gov/articles/how-secure-your-home-wi-fi-network'
    publisher: 'Federal Trade Commission'
    kind: 'regulator'
    accessed: '2026-09-27'
  - title: 'VPN guide'
    url: 'https://ssd.eff.org/module/choosing-vpn-thats-right-you'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    accessed: '2026-09-27'
related:
  guides: ['vpn/what-vpns-do-and-dont', 'dns/dns-privacy', 'operating-systems/hardening-basics']
  archive: []
  news: []
---

## Assume the network can lie

An open or unfamiliar Wi-Fi network can be misconfigured, monitored, impersonated or simply
unreliable. The network operator can usually observe connection metadata such as which systems you
contact, when you connect and how much traffic you exchange. Unencrypted protocols can expose more.

The network name is not proof of identity. An attacker can create a hotspot with the same name as a
hotel, airport or cafe. Automatic connection to remembered networks creates a separate risk because
your device may send probe information or connect without you making a deliberate choice.

## What HTTPS changes

HTTPS protects the contents of a properly authenticated connection from ordinary network observers.
It does not hide every fact about the connection, and it does not make a malicious website safe. Pay
attention to certificate warnings, avoid entering secrets into pages reached through suspicious
links, and keep the browser and operating system updated.

## When a VPN helps

A VPN can move trust from the local network to the VPN provider and encrypt traffic between your
device and the VPN server. That can be useful on an untrusted network. It does not make you
anonymous, and the VPN provider can still learn connection metadata. HTTPS remains important.

## Practical habits

- Disable automatic joining for networks you do not control.
- Use cellular data for sensitive work when that is the safer option.
- Keep file sharing and discovery off on public networks.
- Do not install a certificate, profile or “security helper” just to access Wi-Fi.
- Disconnect when finished and remove networks you will not use again.
