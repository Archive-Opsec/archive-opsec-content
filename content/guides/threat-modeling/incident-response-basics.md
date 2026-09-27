---
title: 'Incident response for ordinary people'
description: 'A calm first-response plan for a stolen device, compromised account, suspicious login or exposed personal information.'
category: 'threat-modeling'
updated: '2026-09-27'
added: '2026-09-27'
author: 'Archive-Opsec contributors'
contributors: []
difficulty: 'intermediate'
tags: ['incident-response', 'threat-model', 'account-security', 'backups']
featured: false
status: 'published'
sources:
  - title: 'Computer Security Incident Handling Guide'
    url: 'https://csrc.nist.gov/pubs/sp/800/61/r2/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Account security guidance'
    url: 'https://consumer.ftc.gov/articles/how-recognize-and-avoid-phishing-scams'
    publisher: 'Federal Trade Commission'
    kind: 'regulator'
    accessed: '2026-09-27'
related:
  guides: ['authentication/account-recovery', 'encryption/secure-backups', 'threat-modeling/define-your-threat-model']
  archive: []
  news: []
---

## Slow down first

An incident creates pressure. Attackers use urgency to keep you from preserving evidence, checking a
message, or asking another person for help. Write down what happened, when you noticed it, which
device or account was involved, and what you have already changed.

## Contain the immediate path

Use a known-clean device to change the most important account password, revoke active sessions,
remove unknown recovery methods, and enable stronger authentication. If a device is stolen, use
the platform's lock or erase controls and contact the carrier when the phone number is involved.

Do not delete every message or wipe the affected device before deciding whether evidence is needed.
If money, abuse, stalking or an active workplace compromise is involved, contact the relevant bank,
platform, employer, or local support service through a verified channel.

## Recover and learn

Restore only from backups you trust. Check for new forwarding rules, browser extensions, OAuth apps,
administrator accounts and unfamiliar devices. Then update the threat model: what was exposed, what
made the event possible, and which control would reduce the chance or impact next time?

:::warning
Do not confront a suspected attacker or publish private evidence while the situation is active.
Preserve what you can and get qualified help when safety, money or legal rights are involved.
:::
