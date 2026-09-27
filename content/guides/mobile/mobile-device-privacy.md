---
title: 'Mobile Device Privacy'
description: 'What a phone knows that a laptop does not, which platform settings matter, and the limits of user control.'
category: 'mobile'
difficulty: 'intermediate'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['mobile', 'metadata', 'data-minimisation', 'fingerprinting']
status: 'published'
sources:
  - title: 'App Tracking Transparency'
    url: 'https://developer.apple.com/documentation/apptrackingtransparency'
    publisher: 'Apple Inc.'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'Apple: Controlling access to information in your apps'
    url: 'https://support.apple.com/guide/iphone/control-access-to-information-in-your-apps-iph251e92810/ios'
    publisher: 'Apple Inc.'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'Android: App permissions'
    url: 'https://support.google.com/android/answer/9431959'
    publisher: 'Google LLC'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'Location Leaks over the GSM Air Interface'
    url: 'https://www.ndss-symposium.org/ndss2012/ndss-2012-programme/location-leaks-over-gsm-air-interface/'
    publisher: 'NDSS Symposium'
    kind: 'academic'
    note: 'Kune, Koelndorfer, Hopper and Kim, NDSS Symposium 2012: mobile networks broadcast subscriber locations over unencrypted signalling, so location is exposed independently of any resettable app-level identifier. Replaces a citation to a paper and DOI that could not be found in the NDSS 2012 proceedings.'
    accessed: '2026-09-27'
related:
  guides:
    [
      'metadata/metadata-explained',
      'operating-systems/hardening-basics',
      'browsers/browser-fingerprinting',
      'authentication/passkeys',
    ]
  archive: []
  news: []
---

A phone is the most capable tracking device most people own, because it is a
camera, a microphone, a location beacon, an account for payment, and a radio that is
identifiable by design. It is also usually the device you cannot replace without losing
your life for a few weeks.

## What the platform already does

**Both platforms encrypt the device at rest** by default, with keys bound to the secure
element. See [full-disk encryption](/guides/operating-systems/full-disk-encryption/).

**Sockets are protected.** Modern mobile networks identify subscribers with temporary
identifiers that rotate, which is a genuine improvement on the permanent identifiers
telephony once required. It also means your carrier can still correlate your activity
over time.

**Advertising identifiers exist** and are resettable. Resetting is worthwhile, but
[Kune et al.](https://www.ndss-symposium.org/ndss2012/ndss-2012-programme/location-leaks-over-gsm-air-interface/)
show that mobile networks themselves leak location over the GSM air interface, in
unencrypted signalling. An identifier you can reset does not help if the network is
publishing where you are anyway.

## Settings worth changing

1. **Location: "While Using" or "Never"**, per app, not system-wide. Most apps do not need
   background location.
2. **Disable ad personalisation and the advertising identifier** where the platform offers
   it.
3. **Revoke permissions you have never seen used.** Camera, microphone, contacts, and
   photos are the usual over-requests.
4. **Turn on app tracking permission prompts** — see
   [App Tracking Transparency](/archive/corporate-privacy/apple-app-tracking-transparency/).
5. **Review cloud backup contents.** A backup can be the least protected copy of
   everything.
6. **Set a short screen-lock timeout**, and require biometrics for the payment app
   specifically.
7. **Check for an IMEI or advertising exposure setting** where your jurisdiction
   requires one to exist; the setting being present is a sign of the law, not of a
   technical protection.

:::warning
Turning off an identifier does not remove data already collected. Platform deletion
requests work, but coverage and retention vary. A
[delete-my-data request](/guides/privacy-basics/harm-reduction/) is worth making for the
accounts that matter most, and worth knowing whether it worked.
:::

## What you cannot fix from settings

- **Preinstalled software**, which is a privileged position the user cannot audit on most
  devices. This is a structural problem, not a settings problem.
- **Advertising in free operating systems.** Some of it is funded by data, and
  [App Tracking Transparency](/archive/corporate-privacy/apple-app-tracking-transparency/)
  and the equivalent Android controls exist because the default is otherwise opt-out.
- **Hardware identifiers at the radio layer.** IMEI, MAC addresses, and nearby
  Bluetooth beacons exist to make the network function. They are the reason a phone cannot
  be made anonymous by configuration.
- **App behaviour that changes after installation.** Permissions are a snapshot; an app
  update can change what it does with them.
- **Someone else's phone.** A large fraction of location data comes from a handset you do
  not control.

:::note
The realistic position is damage limitation: use a device that still receives security
updates, keep permissions minimal, treat the phone as a single point of failure for two
factor, and accept that it is a tracking device that also happens to make most of your
life convenient. Anyone offering to remove that trade-off is usually selling something.
:::

## Reducing the concentration of risk

- Keep a second, older device that you do not use for banking or as a second factor. A
  device used only for travel is a real containment measure.
- Use a hardware key or a passkey for the accounts that matter, so the phone is not the
  only thing that can authorise a login. See
  [passkeys](/guides/authentication/passkeys/).
- Keep a written record of which accounts use the phone as a second factor, so a lost or
  replaced device is a known problem rather than a surprise.

## Sources

- [Apple: App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency)
  — the framework and the permission prompt, in the vendor's own documentation.
- [Apple: Controlling access to information in your apps](https://support.apple.com/guide/iphone/control-access-to-information-in-your-apps-iph251e92810/ios)
  — current permission settings.
- [Google: App permissions](https://support.google.com/android/answer/9431959) — the
  Android permission model and the "special access" list that is easy to miss.
- [Kune et al., _Location Leaks over the GSM Air Interface_](https://www.ndss-symposium.org/ndss2012/ndss-2012-programme/location-leaks-over-gsm-air-interface/) —
  _NDSS Symposium_ 2012. The air-interface signalling leak, independent of app identifiers.
