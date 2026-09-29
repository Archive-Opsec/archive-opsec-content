---
title: 'EternalBlue and Its Use in WannaCry and NotPetya'
description: 'The Windows SMB vulnerability that became the most consequential exploited vulnerability of the 2010s, and the two campaigns built on it.'
category: 'security-incidents'
date: '2026-09-27'
eventDate: '2017-03-14'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'MS17-010, tracked as CVE-2017-0143 and CVE-2017-0144, was a buffer overflow in Server Message Block in Windows. Microsoft released a patch on 14 March 2017. Two campaigns later used it: WannaCry in May 2017 and NotPetya in June 2017. The tooling was later incorporated into publicly available exploit frameworks.'
claims:
  - type: fact
    text: 'The vulnerability is tracked as CVE-2017-0143 (SMBv1 information disclosure) and CVE-2017-0144 (SMBv1 remote code execution).'
  - type: fact
    text: 'Microsoft released security update MS17-010 on 14 March 2017, which required a restart.'
  - type: fact
    text: 'Microsoft had shipped related fixes for EternalBlue in earlier monthly updates, and security researchers later reported that the defect was present in SMB since at least 2008, based on analysis of archived Windows source code.'
  - type: fact
    text: 'NotPetya propagated using MS17-010 together with other techniques, including credential theft, and combined encryption of the master file table with overwriting of the master boot record.'
  - type: fact
    text: 'The WannaCry propagation used MS17-010, and the malware also dropped a patch to prevent further exploitation of the vulnerability on infected machines, which limited re-infection but did not undo the encryption.'
  - type: source-claim
    text: 'The Canadian Centre for Cyber Security stated that it was aware of the statements made by its allies and partners concerning the role of actors in North Korea in the development of the malware known as WannaCry, and that this assessment was consistent with its own analysis. An earlier version of this entry cited a joint NSA, NCSC and CCCS statement also attributing EternalBlue to the Russian military intelligence service; no such statement could be located in a first-party record, so that attribution is not carried here.'
affected:
  - 'Windows systems running SMBv1 that had not applied MS17-010'
dataCategories:
  - 'Not primarily a data exposure event. The risk was unauthorised access, which then creates the possibility of any subsequent data access.'
geographicScope:
  - 'Global'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['x-international']
crossBorder: false
sources:
  - title: 'CVE-2017-0144 — SMB Remote Code Execution Vulnerability'
    url: 'https://msrc.microsoft.com/update-guide/vulnerability/CVE-2017-0144'
    publisher: 'Microsoft Security Response Center'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'Security Update Guide, March 2017'
    url: 'https://msrc.microsoft.com/update-guide'
    publisher: 'Microsoft Security Response Center'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'CSE Statement on the Attribution of WannaCry Malware'
    url: 'https://www.cse-cst.gc.ca/en/information-and-resources/announcements/cse-statement-attribution-wannacry-malware'
    publisher: 'Communications Security Establishment Canada'
    kind: 'government'
    accessed: '2026-09-27'
tags: ['ransomware', 'supply-chain', 'disclosure']
related:
  guides: ['operating-systems/hardening-basics', 'threat-modeling/common-threats']
  archive: ['security-incidents/log4shell', 'security-incidents/colonial-pipeline-2021']
  news: []
---

## The defect

SMBv1 contained a memory management flaw allowing remote code execution. It required three
things to be true of a target: SMB exposed to the network, the patch not applied, and a
listener on port 445. The third is why this was mainly an internet-facing problem and why
segmentation was an effective mitigation.

:::note
The disclosure history is a useful corrective to the idea that vulnerability disclosure
is a simple binary. The flaw had existed for years, was fixed incompletely in a prior
monthly update cycle, and was publicly exploitable and weaponised within two months of the
complete patch. Patch availability and patch application are separate facts.
:::

## WannaCry, May 2017

A ransomware worm using MS17-010 for propagation, with a kill switch consisting of
registered domain checks. It caused reported disruption to healthcare, manufacturing,
telecommunications, and logistics organisations, several of which halted operations on
encrypted systems.

## NotPetya, June 2017

A worm that combined MS17-010 propagation with credential theft and a destructive
filesystem operation. Unlike WannaCry, it had no effective kill switch, and its effects
were not limited to encryption: the master boot record was overwritten and the operating
system was left unbootable in many cases.

## The attribution question

Canada?셲 Communications Security Establishment published a statement noting that it was aware
of the statements made by its allies and partners concerning the role of actors in North Korea
in the development of WannaCry, and that this assessment was consistent with its own
analysis. This is an official government statement, which is why it is recorded here as an
attributed claim rather than as established fact, and it is not accompanied by published
technical evidence. It says nothing about the origin of EternalBlue, which is attributed
elsewhere and is not sourced in this entry.

## Why this entry is grouped the way it is

WannaCry and NotPetya were global events with significant disruption, but they are not
primarily privacy events: the harm was availability, integrity, and physical-world
consequences rather than exposure of personal data. The archive keeps them because they are
the reference cases for patch discipline, not because they belong in a breach count.

## Sources

- [MSRC: CVE-2017-0144](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2017-0144)
  — the vendor record for the flaw and the patch.
- [Security Update Guide](https://msrc.microsoft.com/update-guide) — the authoritative
  record for patch availability, which is the question this incident turns on.
- [CSE: Statement on the Attribution of WannaCry Malware](https://www.cse-cst.gc.ca/en/information-and-resources/announcements/cse-statement-attribution-wannacry-malware)
  — the government attribution, as a source claim.
