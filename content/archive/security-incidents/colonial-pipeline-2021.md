---
title: 'Colonial Pipeline Ransomware Attack'
description: 'The 7 May 2021 ransomware attack on the operator of the largest US fuel pipeline, the ransom payment, and the recovery of most of it.'
category: 'security-incidents'
date: '2026-09-27'
eventDate: '2021-05-07'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'The Colonial Pipeline Company shut down its pipeline operations on 7 May 2021 after an attacker using the DarkSide ransomware family encrypted systems and demanded a ransom. Fuel shortages followed on the US East Coast. The company paid a ransom reported at approximately $4.4 million in bitcoin. The US Department of Justice seized 63.7 bitcoin from that payment in June 2021, then valued at approximately $2.3 million.'
claims:
  - type: fact
    text: 'Colonial Pipeline shut down its pipeline on 7 May 2021 following a ransomware attack, and resumed fuel deliveries over several subsequent days.'
  - type: fact
    text: 'The attacker used the DarkSide ransomware family, and DarkSide affiliates publicly claimed responsibility for the theft of approximately 100 gigabytes of data before the encryption.'
  - type: fact
    text: 'The Department of Justice did not say how the funds were identified, and the recovery was the subject of public speculation that has not been confirmed by the Department.'
  - type: source-claim
    text: 'Reporting at the time, citing unnamed sources and a third-party investigation, stated that the entry point was a legacy VPN account using a single-factor password without multi-factor authentication. Colonial Pipeline has not published a detailed technical postmortem, and this entry does not present that detail as a disclosed fact.'
  - type: researcher-analysis
    text: 'Analysis of DarkSide affiliates and their infrastructure has been published by security researchers, and the incident is a documented case of a criminal ransomware group operating as a service with affiliates who, in this case, publicly negotiated for and attempted to extort payment separately.'
  - type: editorial
    text: 'The lasting significance of this incident is regulatory: it produced a Federal Energy Regulatory Commission enforcement action and testimony in the United States Congress about the cybersecurity requirements for pipeline operators, and it is a common reference point for the argument that ransomware is a threat to critical infrastructure and not only to data.'
affected:
  - 'Colonial Pipeline Company operations and its customers along the US East Coast'
dataCategories:
  - 'The DarkSide affiliate stated that approximately 100 gigabytes of data was stolen before encryption. The composition of that data has not been verified in a public primary record.'
geographicScope:
  - 'Eastern United States'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['us']
crossBorder: false
sources:
  - title: 'Department of Justice Seizes $2.3 Million in Cryptocurrency Paid to the Ransomware Extortionists Darkside'
    url: 'https://www.justice.gov/archives/opa/pr/department-justice-seizes-23-million-cryptocurrency-paid-ransomware-extortionists-darkside'
    publisher: 'US Department of Justice'
    kind: 'government'
    accessed: '2026-09-27'
tags: ['ransomware', 'critical-infrastructure', 'supply-chain']
related:
  guides:
    [
      'authentication/two-factor-authentication',
      'operating-systems/hardening-basics',
      'threat-modeling/define-your-threat-model',
    ]
  archive: ['security-incidents/eternalblue-wannacry-notpetya', 'security-incidents/log4shell']
  news: []
---

## The event

On 7 May 2021, Colonial Pipeline shut down its pipeline, which moves refined fuel and
petroleum products from the Gulf Coast to the East Coast. The shutdown was a decision, and
it was the correct one, but it produced visible fuel shortages and long queues at stations
across several states.

The attacker used DarkSide, which operated as a ransomware-as-a-service arrangement with
affiliates. In this incident, the affiliate both encrypted systems and used a companion
site to publish what it said was stolen data, and used that publication to increase pressure
on the victim to pay.

## The payment and the recovery

Colonial paid the ransom; the reported figure is approximately $4.4 million in bitcoin. The
[US Department of Justice](https://www.justice.gov/archives/opa/pr/department-justice-seizes-23-million-cryptocurrency-paid-ransomware-extortionists-darkside)
announced in June 2021 that it had seized 63.7 bitcoin from the payment, then valued at
approximately $2.3 million. The Department has not published the technical means of the
recovery, and speculation about the mechanism, including reports involving a crypto
exchange, is not confirmed by the Department.

:::note
The ransom payment is a public figure and the recovery is a public figure, and both belong
in this entry. The number of victims, the composition of the stolen data, and the identity
of the individual operators are not established by a primary record, and this entry does not
assert them.
:::

## Entry point, and what is not disclosed

The widely reported account of the entry point is a legacy VPN account with a
single-factor password and no multi-factor authentication. That account is not in a
public primary record. It should be read as reported analysis, and it is notable that the
most useful lesson of the incident is not about ransomware at all but about
[multi-factor authentication](/guides/authentication/two-factor-authentication/) on the
least glamorous system in the estate.

## Regulatory consequence

The incident was followed by a Federal Energy Regulatory Commission enforcement
action and by congressional testimony. Those records are the durable output of the
incident, and they are more useful to a reader than the ransom amount.

## Sources

- [DOJ: Seizure of cryptocurrency paid to the DarkSide extortionists](https://www.justice.gov/archives/opa/pr/department-justice-seizes-23-million-cryptocurrency-paid-ransomware-extortionists-darkside)

  This is the primary record for the payment and the seizure. Root-cause reporting
  attributed to journalists is recorded in the claims above as a source claim.
