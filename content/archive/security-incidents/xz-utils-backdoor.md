---
title: 'xz-utils Backdoor (CVE-2024-3094)'
description: 'A build-time backdoor in liblzma, planted through a multi-year social engineering campaign against a single maintainer, and caught by a performance regression.'
category: 'security-incidents'
date: '2026-09-27'
eventDate: '2024-03-29'
status: 'confirmed'
verification: 'unchecked'
lastVerified: '2026-09-27'
summary: 'A backdoor was introduced into the xz compression library, affecting liblzma 5.6.0 and 5.6.1, and reaching systems indirectly through build-time hooks that patched sshd. It was reported privately on 29 March 2024 by Andres Freund after investigating an unexplained performance and authentication regression, and is tracked as CVE-2024-3094. It was present in development and rolling distribution Linux packages and was not present in current stable releases.'
claims:
  - type: fact
    text: 'The backdoor is tracked as CVE-2024-3094 in the National Vulnerability Database.'
  - type: fact
    text: 'It was disclosed by Andres Freund on 29 March 2024 on the oss-security list, after he had privately reported it to affected distribution maintainers.'
  - type: fact
    text: 'The affected versions are xz 5.6.0 and 5.6.1, and the backdoor is in liblzma, which is a dependency of an unusually large amount of the software ecosystem.'
  - type: fact
    text: 'The backdoor was introduced in the build system, in a build script, rather than in the source of the compression library, and it hooked into sshd through a systemd service patch. Removing the binary artefacts does not remove the modified build path.'
  - type: fact
    text: 'The backdoor was discovered through an unexplained performance and memory-related regression in sshd, and through the failure of a legitimate account to authenticate, rather than through a vulnerability report.'
  - type: fact
    text: 'The two malicious commits, when hashed, produced the same SHA-1 commit object across all repositories, which is an artefact of the object database used by the hosting service and was one of the strongest available signals that the commits did not originate upstream.'
  - type: researcher-analysis
    text: 'Independent analysis described the two-year campaign attributed to the persona "Jia Tan", the pressure applied to the maintainer, and the long tail of deliberately innocuous commits. The maintainer, Lasse Collin, has stated that he was not aware the changes were malicious and that he was under substantial pressure from a third party claiming to work with security researchers.'
  - type: fact
    text: 'Red Hat, Debian, Fedora, Ubuntu, SUSE, openSUSE, and others shipped or avoided the affected development packages. Some distributions reverted the packages as a precaution, and some rewrote the affected files because the tarball artefacts were not a complete description of the change.'
  - type: source-claim
    text: 'There is no public primary record of who was behind the "Jia Tan" account or of the campaign behind it. Any attribution in circulation is inference, not disclosure.'
affected:
  - 'Linux distributions shipping xz 5.6.0 or 5.6.1, primarily development, testing and rolling releases, during the period the affected packages were live'
  - 'Indirectly, any software that linked liblzma'
dataCategories:
  - 'The published technical analyses concern the ability of the backdoor to pass through SSH authentication. No primary record establishes that it was used against a specific victim.'
geographicScope:
  - 'Global'

# Structured jurisdiction, from src/data/jurisdictions.json. Drives the region and
# country filters; geographicScope above stays as the prose record.
jurisdictions: ['x-international']
crossBorder: false
sources:
  - title: 'CVE-2024-3094'
    url: 'https://nvd.nist.gov/vuln/detail/CVE-2024-3094'
    publisher: 'National Vulnerability Database'
    kind: 'government'
    accessed: '2026-09-27'
  - title: 'oss-security announcement: backdoor in xz 5.6.0 and 5.6.1'
    url: 'https://www.openwall.com/lists/oss-security/2024/03/29/4'
    publisher: 'Andres Freund, via the oss-security list'
    kind: 'documentation'
    note: 'The original technical disclosure.'
    accessed: '2026-09-27'
  - title: 'CISA Advisory AA24-131A, Backdoor in XZ Utils Data Compression Library, CVE-2024-3094'
    url: 'https://www.cisa.gov/news-events/cybersecurity-advisories/aa24-131a'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-09-27'
tags: ['supply-chain', 'disclosure', 'hardening']
related:
  guides:
    [
      'operating-systems/hardening-basics',
      'encryption/encryption-explained',
      'threat-modeling/common-threats',
    ]
  archive:
    [
      'security-incidents/log4shell',
      'security-incidents/solarwinds-sunburst',
      'security-incidents/heartbleed',
    ]
  news: []
---

## Why this entry is in a privacy and security archive

The backdoor's interest is not that it was caught before use, which is a matter of research
outcome, but that it shows the actual attack surface. A single unpaid volunteer was the
weak point, and the attacker attacked the maintainer, not the code.

## What was actually done

Three things, and the combination matters more than any of them:

1. **Social engineering over years.** A convincing contribution history was built up over
   roughly two years, under pressure, using accounts in the project's public space.
2. **Compromise of the build.** The backdoor was placed in build configuration so that it
   was compiled into artefacts rather than visible in the library source. The malicious
   commits were identical across repositories in a way that betrayed the origin.
3. **Hooking a privileged service.** The build artefacts hooked into `sshd` through a
   systemd service patch, so that the backdoor ran in the SSH authentication path of every
   host that installed the package.

## Discovery

The detection that led to the report was a performance regression: a syscall difference
observable in `perf` output, and an authentication attempt for a legitimate account that
failing in a way that should not have happened. Andres Freund followed the anomaly back
through the build path.

This is worth saying plainly: the near miss is a matter of luck plus a specific technical
observation. There is no monitoring control that reliably detects a backdoor in this
position.

:::warning
The practical lesson for a reader is narrow and uncomfortable. The trusted distribution
chain, the maintainer, the code review process, and the package signature were all working
as designed. The attacker operated inside the design. Reviewing change provenance and
questions of who is actually behind an identity is the control that helped here, and it is
not automatable in a way that scales.
:::

## No victim, no victim count

There is no primary record of exploitation against a specific organisation in the public
disclosure. The affected packages were primarily development and rolling distribution
channels. The correct statement is that the backdoor was found before verified exploitation
in production systems, and this entry will be updated if that changes.

## Sources

- [NVD: CVE-2024-3094](https://nvd.nist.gov/vuln/detail/CVE-2024-3094) — the canonical
  record.
- [oss-security disclosure](https://www.openwall.com/lists/oss-security/2024/03/29/4) — the
  original technical description by the reporter, and the best available primary record.
- [CISA advisory AA24-131A](https://www.cisa.gov/news-events/cybersecurity-advisories/aa24-131a)
  — the government response and affected distribution guidance.
