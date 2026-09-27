---
title: 'Operating System Hardening Basics'
description: 'A short, durable hardening routine: updates, permissions, encryption, telemetry, and what to leave alone.'
category: 'operating-systems'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['hardening', 'encryption', 'open-source', 'data-minimisation']
status: 'published'
sources:
  - title: 'CIS Benchmarks'
    url: 'https://www.cisecurity.org/cis-benchmarks'
    publisher: 'Center for Internet Security'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'NIST SP 800-147: BIOS Protection Guidelines'
    url: 'https://csrc.nist.gov/pubs/sp/800/147/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'Microsoft Security Baselines'
    url: 'https://www.microsoft.com/en-us/download/details.aspx?id=55319'
    publisher: 'Microsoft Corporation'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'Apple Platform Security'
    url: 'https://support.apple.com/guide/security/'
    publisher: 'Apple Inc.'
    kind: 'company'
    accessed: '2026-09-27'
related:
  guides:
    [
      'operating-systems/full-disk-encryption',
      'mobile/mobile-device-privacy',
      'encryption/encryption-explained',
      'password-managers/using-a-password-manager',
    ]
  archive: ['security-incidents/solarwinds-sunburst', 'security-incidents/log4shell']
  news: []
---

Hardening is the unglamorous work that determines how much damage a mistake can do. Most
of it is a one-time configuration that is then maintained by updates. Most of it is also
documented by somebody, so you do not have to invent it.

## 1. Automatic updates, on everything

Operating system, browser, router, and anything with a firmware image. Enable automatic
security updates and check that they are actually succeeding — silent failures are common
on locked-down networks.

:::warning
The [Log4Shell](/archive/security-incidents/log4shell/) and
[SUNBURST](/archive/security-incidents/solarwinds-sunburst/) entries are in the archive
because the window between disclosure and exploitation was short. Both were patchable.
:::

## 2. Full-disk encryption, and the recovery key somewhere else

BitLocker, FileVault, or LUKS. Then store the recovery key in a password manager or
printed and kept physically safe. An encrypted disk with a lost recovery key is a brick,
and that is a support problem, not a security failure.

## 3. Full-disk access control

A Windows account in the Administrators group, or a Linux user in `sudo`, can read and
modify everything. Day-to-day use belongs in a standard account. This is the control that
limits the blast radius of malware, and it costs nothing.

```bash
# Linux: confirm you are not running as root in an everyday shell
id -u
groups | tr ' ' '\n' | grep -E '^(sudo|wheel|admin)$'
```

## 4. Secure boot and verified firmware

Secure boot refuses to load an unsigned bootloader, which is what stops a
[supply-chain](/archive/security-incidents/xz-utils-backdoor/) implant from persisting
across reboots. NIST's
[SP 800-147](https://csrc.nist.gov/pubs/sp/800/147/final) is the reference for what a
protected firmware interface should guarantee.

## 5. Lock the screen

Short automatic lock, a strong password or biometric, and no window previews on the lock
screen. A short lock interval is a bigger practical gain than most software hardening.

## 6. Turn down telemetry, knowingly

- Disable customer-experience and diagnostic uploads where the setting exists.
- Disable crash reporting you do not need.
- Review what your desktop OS sends about search, location, and typing suggestions.

:::note
This is where to be careful about the trade-off. Some telemetry settings also control
security telemetry, and some "disable diagnostics" paths affect update delivery. Change
one setting at a time and confirm updates still work.
:::

## 7. Reduce the attack surface you do not use

- Run services as non-root.
- Bind services to `localhost` rather than `0.0.0.0` unless remote access is required.
- Keep the guest operating system and the host isolated.
- Uninstall software rather than merely disabling it, if you no longer need it.

## 8. Backups you have actually tested

Three copies, two media, one off-site. A ransomware payload that encrypts your home
directory is only useful because most people have one copy, on the same disk. See the
[security incidents archive](/archive/security-incidents/) for what has actually been used
in the wild.

## What to leave alone

- **Do not disable security features you do not understand** to make a benchmark number
  go up. CIS and vendor baselines are starting points, and their "recommended" profiles
  are written for environments more hostile than a laptop.
- **Do not run a daily-driver daily build of a cutting-edge release.** You will spend your
  time on breakage instead of on threats.
- **Do not install hardening scripts from a stranger's repository** without reading every
  line. A hardening script runs as administrator by design; that is exactly the thing you
  are trying to avoid.

:::tip
A reasonable target: automatic updates on, disk encrypted, a standard account for daily
use, screen lock in a minute, telemetry reduced, and tested backups. That is most of the
value, and it is five settings rather than five hundred.
:::
