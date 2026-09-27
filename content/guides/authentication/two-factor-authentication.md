---
title: 'Two-Factor Authentication'
description: 'A ranked comparison of second factors, how each fails, and how to recover access without losing the account.'
category: 'authentication'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['totp', 'authentication', 'password-manager']
status: 'published'
sources:
  - title: 'RFC 6238: TOTP: Time-Based One-Time Password Algorithm'
    url: 'https://www.rfc-editor.org/rfc/rfc6238'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'RFC 4226: HOTP'
    url: 'https://www.rfc-editor.org/rfc/rfc4226'
    publisher: 'IETF'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'CISA: More than a Password'
    url: 'https://www.cisa.gov/mfa'
    publisher: 'Cybersecurity and Infrastructure Security Agency'
    kind: 'government'
    accessed: '2026-09-27'
related:
  guides: ['authentication/passkeys', 'password-managers/using-a-password-manager']
  archive: []
  news: []
---

A second factor is the control that most reduces account takeover, because it works even
after your password has been reused, phished, or leaked. Which one you choose is a
question about how each fails.

## The options, weakest to strongest

**SMS codes.** Vulnerable to SIM swapping, to an attacker with your phone number, and to
any interception weakness in the carrier's network. Acceptable only where a service offers
nothing better and the account is low-value.

**Email codes.** Equivalent in strength to your email account, which makes it circular:
it is only as strong as the thing that resets it. Better than SMS, still not good.

**TOTP from an authenticator app.** A six-digit code derived from a shared secret and the
current time, standardised in
[RFC 6238](https://www.rfc-editor.org/rfc/rfc6238). Codes are 30 or 60 seconds long and
can be replayed within that window, but they cannot be phished and they work with no
network. **This is the sensible default.**

**Push approval.** A notification you approve on another device. Convenient, and the
weakest of the "app" options, because approval requests can be pushed to a real device
and a user can be talked into approving one. Treat as a step up from SMS, not as an
equivalent to TOTP.

**Hardware security keys and passkeys.** A cryptographic key exchange rather than a
secret, bound to a domain, and therefore unusable by a phishing site. Strongest option.
See [passkeys](/guides/authentication/passkeys/).

:::warning
Watch for the one thing that matters more than which factor you chose: an unexpected
prompt means your password is already stolen. Deny it, then reset that password
immediately. If prompts you did not trigger keep arriving, assume the account is
compromised rather than a glitch.
:::

## Turn it on in the right order

1. Your email provider. It is the account that resets the others.
2. Your bank and any account holding payment details.
3. Your password manager, if it supports it.
4. Your operating system account.
5. Everything else that offers it, prioritised by what an attacker would want.

## Recovery, before you need it

- Save the generated recovery codes and store them in your password manager, not on a
  sticky note and not in the same account.
- Register a second factor — a second authenticator, a second key — where the service
  allows it. Single-factor-of-two lockouts are the main practical failure mode.
- Check the service's recovery flow _now_. If it is "we email you a link", then the
  account's real security is the security of your email account.
- Keep a record of which accounts still have SMS as the only option. That list is a
  to-do list.

## What 2FA does not fix

- **Credential phishing on services that only ask for a password.** Use a password
  manager that matches the origin.
- **Session theft.** A cookie stolen after a successful login needs no second factor.
  See [end-to-end encrypted messaging](/guides/messaging/end-to-end-encrypted-messaging/)
  for the equivalent problem in messaging.
- **A compromised device.** An attacker with code execution as you bypasses the prompt.
- **A support agent who resets the account for a convincing story.** Social engineering
  of support is a real vector; a support process that will reset MFA on request is the
  weak point, not the factor.

## Sources

- [RFC 6238](https://www.rfc-editor.org/rfc/rfc6238) — the TOTP standard, including the
  time-step and replay considerations.
- [RFC 4226](https://www.rfc-editor.org/rfc/rfc4226) — HOTP, the counter-based
  predecessor.
- [CISA: More than a Password](https://www.cisa.gov/mfa) — a short, vendor-neutral
  explanation of why MFA works and how to deploy it without locking yourself out.
