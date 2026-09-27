---
title: 'SolarWinds SUNBURST'
description: 'A malicious update distributed through SolarWinds Orion, attributed publicly to a named threat actor, and the disclosure that followed.'
category: 'security-incidents'
date: '2026-09-27'
eventDate: '2020-12-04'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'A trojanised update to the SolarWinds Orion platform was distributed to organisations that installed versions 2019.4 HF5 through 2020.2.1 HF1. The implant, dubbed SUNBURST by FireEye and GOLDEN SAML by Microsoft, performed reconnaissance and exfiltration. CISA issued Emergency Directive 21-01 on 13 December 2020.'
claims:
  - type: fact
    text: 'SolarWinds disclosed on 13 December 2020 that versions 2019.4 HF5 through 2020.2.1 HF1 of Orion had been affected by a compromise of its build and release process.'
  - type: fact
    text: 'CISA issued Emergency Directive 21-01, Mitigate SolarWinds Orion Code Compromise, on 13 December 2020.'
  - type: fact
    text: 'FireEye published an analysis naming the implant SUNBURST on 13 December 2020 and reported that the actor it referred to as UNC2452 had stolen security certificates from multiple organisations to forge SAML tokens.'
  - type: fact
    text: 'Microsoft published an analysis on 18 December 2020 describing the implant under the name GOLDEN SAML and the actor as Nobelium, and stated that the campaign began with test access in 2018 and moved to Orion in 2019.'
  - type: fact
    text: 'SolarWinds SEC filings in December 2020 described the compromise and its own investigation. The company reported significant financial impact in later filings, and the figures evolved across filings; consult the filings rather than summaries.'
  - type: researcher-analysis
    text: 'Multiple independent analyses found that the implant was narrowly targeted, with a filter preventing it from operating on clearly non-target systems, which is consistent with intelligence-collection tradecraft rather than indiscriminate deployment.'
  - type: source-claim
    text: 'Attribution to the Russian SVR, the agency responsible for the 2016 theft of security materials attributed to the same service, is made in the United States, United Kingdom, Canada, Australia, New Zealand, and EU statements, and in private-sector analyses. The evidence has not been published in full.'
affected:
  - 'Federal, state, local and foreign government agencies'
  - 'Private sector organisations, including security vendors, defence contractors, telecommunications firms, and financial institutions'
dataCategories:
  - 'Credentials and tokens, including forged authentication tokens'
  - 'Mail data, where the implant was deployed against mail servers'
geographicScope:
  - 'United States'
  - 'Western Europe'
  - 'Australia'
  - 'New Zealand'
sources:
  - title: 'Emergency Directive 21-01: Mitigate SolarWinds Orion Code Compromise'
    url: 'https://www.cisa.gov/news-events/directives/ed-21-01-mitigate-solarwinds-orion-code-compromise'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'SolarWinds SEC filings (EDGAR company filing index, CIK 1739942)'
    url: 'https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=0001739942&type=8-K&dateb=&owner=include&count=40'
    publisher: 'US Securities and Exchange Commission'
    kind: 'regulator'
    accessed: '2026-09-27'
  - title: 'Highly Evasive Attacker Leverages SolarWinds Supply Chain to Compromise Multiple Global Victims With SUNBURST Backdoor'
    url: 'https://cloud.google.com/blog/topics/threat-intelligence/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor'
    publisher: 'Google Cloud'
    kind: 'company'
    accessed: '2026-09-27'
  - title: 'Analyzing Solorigate, the compromised DLL file that started a sophisticated cyberattack, and how Microsoft Defender helps protect customers'
    url: 'https://www.microsoft.com/en-us/security/blog/2020/12/18/analyzing-solorigate-the-compromised-dll-file-that-started-a-sophisticated-cyberattack-and-how-microsoft-defender-helps-protect'
    publisher: 'Microsoft'
    kind: 'company'
    accessed: '2026-09-27'
tags: ['supply-chain', 'disclosure', 'mass-surveillance']
related:
  guides:
    [
      'operating-systems/hardening-basics',
      'threat-modeling/common-threats',
      'encryption/key-management',
    ]
  archive: ['security-incidents/log4shell', 'security-incidents/xz-utils-backdoor']
  news: []
---

## What happened

A build system used to produce SolarWinds Orion updates was accessed, and malicious code was
injected into the build process so that a signed, trusted update distributed to customers
carried a backdoor. The customers were, in effect, installing the compromise themselves.

The affected versions were 2019.4 HF5 through 2020.2.1 HF1. The 2020.2 HF2 and 2020.2.1
HF2 releases removed the trojanised component.

## Why it mattered

Three properties combined in a way that had not been seen before at this scale:

1. **Trust in the distribution channel.** The update was signed and delivered through the
   vendor?셲 normal process. Signature checking did not help, because the signature was
   valid.
2. **Concentration.** Orion was used for network management by a large number of
   organisations, including security vendors whose visibility would make a foothold
   valuable.
3. **Consequential stolen artefacts.** The actor used the access to take security
   certificates and forge authentication tokens, which turns a network foothold into
   access to identity providers and cloud services.

:::warning
This is the clearest documented case of an attacker using a software vendor?셲 build
pipeline as the delivery mechanism. A compromise of the build environment is a compromise
of every customer who updates, and no amount of endpoint hardening on the customer side
defends against it. The controls that help are upstream: reproducible builds, build
environment isolation, transparency logs, and monitoring for exactly this pattern.
:::

## Attribution

The attribution to the Russian Foreign Intelligence Service was announced by the
[Emergency Directive 21-01](https://www.cisa.gov/news-events/directives/ed-21-01-mitigate-solarwinds-orion-code-compromise)
memorandum and by parallel statements from the United Kingdom, Canada, Australia, New
Zealand, and the European Union, and is repeated in the private-sector analyses cited
above. The technical evidence is published in outline; the intelligence that supported the
identification is not. As always on this site, an official attribution is recorded as a
source claim.

## Records

The company?셲 own filings with the
[US Securities and Exchange Commission](https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=0001739942&type=8-K&dateb=&owner=include&count=40)
are the primary record for what SolarWinds knew, when, and what it cost. The
[Mandiant analysis](https://cloud.google.com/blog/topics/threat-intelligence/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor)
and the [Microsoft analysis](https://www.microsoft.com/en-us/security/blog/2020/12/18/analyzing-solorigate-the-compromised-dll-file-that-started-a-sophisticated-cyberattack-and-how-microsoft-defender-helps-protect)
are the primary records for the technical detail. Press summaries should be checked against
these.

## Sources

- [CISA Emergency Directive 21-01](https://www.cisa.gov/news-events/directives/ed-21-01-mitigate-solarwinds-orion-code-compromise)
  — the directive text and the attribution statement.
- [SEC EDGAR: SolarWinds filings](https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=0001739942&type=8-K&dateb=&owner=include&count=40)
  — the company?셲 own disclosures.
- [Mandiant: Highly Evasive Attacker Leverages SolarWinds Supply Chain](https://cloud.google.com/blog/topics/threat-intelligence/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor)
  — the SUNBURST analysis and the certificate-theft findings.
- [Microsoft: Analyzing Solorigate](https://www.microsoft.com/en-us/security/blog/2020/12/18/analyzing-solorigate-the-compromised-dll-file-that-started-a-sophisticated-cyberattack-and-how-microsoft-defender-helps-protect)
  — the GOLDEN SAML and Nobelium analysis, including the timeline back to 2018.
