---
title: 'Software updates and the security window'
description: 'Why updates matter, how to make them routine, and how to handle devices that no longer receive security fixes.'
category: 'operating-systems'
updated: '2026-09-27'
added: '2026-09-27'
author: 'Archive-Opsec contributors'
contributors: []
difficulty: 'introductory'
tags: ['updates', 'hardening', 'security', 'operating-systems']
featured: false
status: 'published'
sources:
  - title: 'Update software'
    url: 'https://www.cisa.gov/secure-our-world/update-software'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'Common Vulnerabilities and Exposures'
    url: 'https://www.cve.org/'
    publisher: 'MITRE'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides: ['operating-systems/hardening-basics', 'operating-systems/full-disk-encryption']
  archive: ['security-incidents/log4shell', 'security-incidents/heartbleed']
  news: []
---

## The security window

An update closes some known problems; it does not make a device permanently secure. The useful
question is whether a device is receiving fixes in time for the threats that matter to you. A
device that no longer receives security updates belongs in a different threat model from a current
device.

Enable automatic updates where they are reliable and compatible with your work. If updates must be
managed manually, choose a regular schedule and check the operating system, browser, firmware,
applications and extensions separately.

## What to do when an update breaks something

Do not disable updates permanently because of one failure. Keep a tested backup, read the vendor's
release notes, and separate the affected device from sensitive work until a fix is available. A
temporary delay can be reasonable; an indefinite delay turns a known vulnerability into a standing
exposure.

## Retire unsupported devices

If a phone, router, browser or operating system has reached end of support, replace it or isolate it
from sensitive activity. Removing unused software and accounts reduces the attack surface but does
not replace security patches.

:::note
The date an update was published is not the same as the date your device installed it. Check the
installed version and reboot when the platform requires it.
:::
