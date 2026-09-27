---
title: 'Define Your Threat Model'
description: 'Work out who you are protecting something from before you install anything, using a written, revisable model.'
category: 'threat-modeling'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['threat-model', 'risk-management']
featured: true
status: 'published'
sources:
  - title: 'Surveillance Self-Defense: Your Security Plan'
    url: 'https://ssd.eff.org/module/your-security-plan'
    publisher: 'Electronic Frontier Foundation'
    kind: 'ngo'
    note: 'EFF renamed this module from "Threat Modeling"; it is the same guide.'
    accessed: '2026-09-27'
  - title: 'NIST SP 800-30 Rev. 1: Guide for Conducting Risk Assessments'
    url: 'https://csrc.nist.gov/pubs/sp/800/30/r1/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'OWASP Threat Modeling Cheat Sheet'
    url: 'https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html'
    publisher: 'OWASP'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides: ['threat-modeling/common-threats', 'privacy-basics/what-privacy-means']
  archive: []
  news: []
---

A threat model is a written answer to three questions: what am I protecting, from whom,
and what happens if I fail? It is not a document you publish. It is a short note that
stops you from buying the wrong tool.

## The three questions

**What am I protecting?** A device, an account, a relationship, a document, your physical
safety, your right to say something. "My privacy" is not an answer, because it does not
imply a single control.

**From whom?** Name a category, and be honest about capability:

| Adversary                        | Typical capability                            | Realistic goal                                              |
| -------------------------------- | --------------------------------------------- | ----------------------------------------------------------- |
| Automated crawlers               | Your browser fingerprint, IP address, cookies | Stop fingerprinting, block third parties                    |
| Data brokers                     | Records bought and sold legally               | Opt out, reduce footprint, avoid new disclosures            |
| A curious network                | Sees DNS, TLS SNI, timing, volume             | Encrypted DNS, encrypted transport, Tor                     |
| A service you depend on          | Sees everything you do on its platform        | Minimise what you give it                                   |
| A targeted attacker              | Phishing, malware, persistent access          | MFA, updates, backups, compartmentalisation                 |
| A state actor with legal process | Subpoenas, warrants, bulk programmes          | Compartmentalisation, encryption, Tor, reducing what exists |
| A physical attacker              | Your unlocked device                          | Full-disk encryption, screen lock, remote wipe              |

**What is failure?** If the answer is "someone reads my messages", the control is
encryption. If it is "someone follows me home", the control is different. If it is "I
cannot log in", the control is a recovery method you have tested.

:::note
Write the failure condition down as a sentence you would be willing to show someone. If
the sentence is vague enough to mean anything, the model is not finished.
:::

## Assets, adversaries, capabilities, exposure

The four columns work for almost anything:

- **Asset** — the thing: a specific account, a device, a location pattern, a set of files.
- **Adversary** — who wants it, from the table above.
- **Capability** — what they can reach: your device only, your accounts, your network
  path, a legal order, a supply chain.
- **Exposure** — how they get in: phishing, a reused password, an unpatched browser, a
  plaintext file, a rogue USB device, a shared document.

Then, for each combination, a decision: accept, reduce, transfer, or avoid. _Accepting_ a
risk explicitly is a legitimate outcome; it is what stops you from spending a week on a
threat you will never meet.

## Review it, and keep it in the repository

Threat models go stale the moment your life changes: a new job, a new city, a new
device, a new dependency. Keep it in your notes or your repository next to the thing it
describes, and revisit it when any of those change.

:::tip
Write it as a bulleted list, not a document. The value is in forcing the decisions, not
in the artefact. Five lines that say "I do not need anonymity from my network, I do need
my accounts secure from a stolen laptop" beats a polished threat model you wrote once.
:::

## Sources

- [EFF Surveillance Self-Defense, Your Security Plan](https://ssd.eff.org/module/your-security-plan)
  — a step-by-step method for personal security, freely available.
- [NIST SP 800-30 Rev. 1](https://csrc.nist.gov/pubs/sp/800/30/r1/final) — the standard
  risk-assessment vocabulary, if you want the formal version.
- [OWASP Threat Modeling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html)
  — aimed at software, useful for the asset/entry-point decomposition.

Next: [common threats, and which of them are worth doing anything about](/guides/threat-modeling/common-threats/).
