---
title: 'Log4Shell (CVE-2021-44228)'
description: 'A remotely exploitable JNDI lookup in Apache Log4j 2, the disclosure-to-exploitation window, and the supply chain behind it.'
category: 'security-incidents'
date: '2026-09-27'
eventDate: '2021-12-10'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'Apache Log4j 2 message lookup functionality evaluated attacker-controlled strings in logged data, allowing a JNDI lookup and, in common configurations, remote code execution. It was assigned CVE-2021-44228, publicly disclosed on 9 December 2021, and the Apache Log4j project issued fixes the same day. It was found to be present in thousands of products, not only in direct Log4j deployments.'
claims:
  - type: fact
    text: 'The vulnerability is tracked as CVE-2021-44228 in the National Vulnerability Database.'
  - type: fact
    text: 'It affects Apache Log4j 2 versions 2.0-beta9 through 2.14.1, as stated in the Apache Log4j project security advisory.'
  - type: fact
    text: 'The flaw was in the message lookup mechanism, where a logged string could be interpreted as a format pattern that triggered a JNDI lookup.'
  - type: fact
    text: 'Apache Log4j 2.15.0 removed the behaviour, and 2.16.0 was released to remove a further vector found in 2.15.0, with 2.17.0 completing the fixes for the family of issues.'
  - type: fact
    text: 'The flaw was also present in products that bundled Log4j rather than exposing it directly, and Apache published a list of affected third-party products.'
  - type: fact
    text: 'Log4j is maintained by the Apache Software Foundation, and Log4j 1.x reached end of life before this incident.'
  - type: researcher-analysis
    text: 'Scanning studies published by researchers in December 2021 estimated that a very large number of internet-facing services were running a vulnerable version. The estimates differ by an order of magnitude between studies, and none is an authoritative count.'
  - type: editorial
    text: 'This entry takes the view that the incident is a supply chain and maintenance problem rather than a vulnerability problem: a mature, widely deployed, end-of-life logging library was in the dependency tree of a large fraction of the industry.'
affected:
  - 'Organisations running Apache Log4j 2, directly or transitively, in internet-facing services'
  - 'Vendors who bundled Log4j 2 into their own products'
dataCategories:
  - 'Not primarily a data exposure event. The risk was code execution, which then creates the possibility of any subsequent data access.'
geographicScope:
  - 'Global'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['x-international']
crossBorder: false
sources:
  - title: 'CVE-2021-44228'
    url: 'https://nvd.nist.gov/vuln/detail/CVE-2021-44228'
    publisher: 'National Vulnerability Database'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'Apache Log4j Security — official project page'
    url: 'https://logging.apache.org/log4j/2.x/security.html'
    publisher: 'The Apache Software Foundation'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'CISA Cybersecurity Advisory AA21-356A, Mitigating Log4Shell and Other Log4j-Related Vulnerabilities'
    url: 'https://www.cisa.gov/news-events/cybersecurity-advisories/aa21-356a'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-09-27'
tags: ['supply-chain', 'ransomware', 'hardening']
related:
  guides:
    [
      'operating-systems/hardening-basics',
      'encryption/encryption-explained',
      'threat-modeling/common-threats',
    ]
  archive:
    [
      'security-incidents/heartbleed',
      'security-incidents/solarwinds-sunburst',
      'security-incidents/xz-utils-backdoor',
    ]
  news: []
---

## The flaw

Log4j 2 supported a message lookup mechanism: text written in a log message could be
interpreted as a pattern that looked up a value. Combined with a JNDI provider on the
classpath, an attacker who can cause a string to be logged — which is most user input,
somewhere — can cause the application to make a lookup, and in widely used configurations
to instantiate objects from the result.

The two conditions that made it exceptional:

1. **Reachability.** Any application that logs user-controlled text was potentially
   vulnerable, which is a large set of applications.
2. **Invisibility.** Log4j configuration is frequently not under the control of the team
   deploying the application, and a vulnerable copy can be present without anyone on the
   team knowing.

## Timeline

| Date       | Event                                                                                                           |
| ---------- | --------------------------------------------------------------------------------------------------------------- |
| 2021-12-09 | Public disclosure; Apache Log4j 2.15.0 released                                                                 |
| 2021-12-10 | Further vector found in 2.15.0; 2.16.0 released                                                                 |
| 2021-12-13 | 2.17.0 released, completing the fixes for the family                                                            |
| 2021-12    | CISA and national CERTs issue alerts; the vulnerability is added to the Known Exploited Vulnerabilities catalog |

The short interval between disclosure and observed exploitation is the finding that
matters most for practice, and it is the reason
[automatic updates](/guides/operating-systems/hardening-basics/) are not optional.

## The second-order lesson

The interesting part of this incident is not the vulnerability. It is that a large
proportion of affected organisations discovered they had a vulnerable copy of a library
they had never chosen, had never audited, and could not have removed in time. The
[practical response](https://www.cisa.gov/news-events/cybersecurity-advisories/aa21-356a)
was to inventory rather than to patch, because the first question was always "where is this
dependency".

## What this entry does not claim

- **No victim count.** The published figures come from research scanning, they disagree
  substantially, and none of them is a census. Anyone quoting a single definitive number
  is quoting a scan.
- **No confirmed attribution of any specific incident to Log4Shell** in this entry.
  Individual crime reports have been linked by investigators, but that linkage belongs in
  an entry about that incident, with its own evidence.

## Sources

- [NVD: CVE-2021-44228](https://nvd.nist.gov/vuln/detail/CVE-2021-44228) — the record, with
  CVSS scoring and references.
- [Apache Log4j security page](https://logging.apache.org/log4j/2.x/security.html) — the
  project's own list of affected versions, fixed versions, and mitigations. Authoritative
  for "is this version vulnerable".
- [CISA advisory AA21-356A](https://www.cisa.gov/news-events/cybersecurity-advisories/aa21-356a)
  — the government response and recommended mitigations.
