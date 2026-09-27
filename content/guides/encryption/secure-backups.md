---
title: 'Secure backups that survive device loss'
description: 'A practical backup plan for recovering important data without turning every copy into an unprotected leak.'
category: 'encryption'
updated: '2026-09-27'
added: '2026-09-27'
author: 'Archive-Opsec contributors'
contributors: []
difficulty: 'intermediate'
tags: ['backups', 'encryption', 'ransomware', 'key-management']
featured: false
status: 'published'
sources:
  - title: 'Ransomware Guide'
    url: 'https://www.cisa.gov/stopransomware/ransomware-guide'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'Contingency Planning Guide for Federal Information Systems'
    url: 'https://csrc.nist.gov/pubs/sp/800/34/r1/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
related:
  guides: ['operating-systems/full-disk-encryption', 'encryption/key-management', 'threat-modeling/define-your-threat-model']
  archive: ['security-incidents/colonial-pipeline-2021', 'security-incidents/xz-utils-backdoor']
  news: []
---

## The backup has to be usable

A backup is not a pile of files. It is a tested ability to restore the right data after a lost
device, failed disk, ransomware event, account lockout or accidental deletion. Start by listing the
data that would be difficult or impossible to recreate: photographs, identity records, recovery
codes, source files, documents and configuration.

## Use more than one copy

Keep multiple copies in different failure domains. A practical pattern is a working copy, a local
backup, and an offline or separately authenticated copy. A second disk next to the computer is
useful against drive failure but not against theft, fire or ransomware that can reach mounted
backups.

Backups should be versioned when possible. If corruption or encryption is discovered late, the
latest copy may already contain the problem. Keep at least one copy that is not continuously
connected or writable by the everyday account.

## Encrypt and practise recovery

Encrypt portable and cloud backups, but document how the key is recovered. A backup encrypted with
a key that exists only on the lost device is not a recovery plan. Store recovery material separately
and protect it against unauthorised access. Test restoration on a spare device or temporary
directory; a backup that has never been restored is an assumption.

:::note
Do not confuse full-disk encryption with backup encryption. Disk encryption protects a device at
rest. It does not protect an exported backup after it leaves that device.
:::

## What to record

Record the backup locations, schedule, retention period, encryption method, recovery owner and last
successful restore. Keep the record short and avoid putting secret keys in the same document.
