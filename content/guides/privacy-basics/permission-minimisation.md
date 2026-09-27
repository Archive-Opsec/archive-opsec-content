---
title: 'Permission minimisation'
description: 'A practical way to decide which apps and services should access location, contacts, files, microphones and cameras.'
category: 'privacy-basics'
updated: '2026-09-27'
added: '2026-09-27'
author: 'Archive-Opsec contributors'
contributors: []
difficulty: 'introductory'
tags: ['data-minimisation', 'mobile', 'permissions', 'privacy']
featured: false
status: 'published'
sources:
  - title: 'Control access to information in apps'
    url: 'https://support.apple.com/guide/iphone/control-access-to-information-in-apps-iph251e92810/ios'
    publisher: 'Apple Support'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'Android permissions'
    url: 'https://support.google.com/android/answer/9431959'
    publisher: 'Google Android Help'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides: ['mobile/mobile-device-privacy', 'privacy-basics/data-brokers-and-data-sale']
  archive: ['corporate-privacy/apple-app-tracking-transparency']
  news: []
---

## Permission is a decision, not a button

When an app asks for access, decide whether the feature you want actually requires the permission.
A map may need location while it is in use. A flashlight usually does not need contacts. A photo
editor may need one selected file rather than the entire photo library.

Grant the narrowest scope available: one-time location instead of always, selected photos instead of
the whole library, and approximate location instead of precise location when the task allows it.

## Review later

Permissions accumulate. Review them after installing a new app, changing phones, or noticing that
an app has not been used for months. Revoke access that no longer matches a current purpose. A
revoked permission may break a feature; that is useful information about what the app depends on.

## Separate the app from the account

Changing a device permission does not erase data already uploaded to the service. Check the account's
privacy controls separately, and delete stored data when the service provides a meaningful option.
The app may also collect information through analytics or advertising systems that do not appear as
a sensor permission.

:::tip
If an app refuses to work without an unrelated permission, look for a web version or a different
tool. Convenience is not evidence that the access is necessary.
:::
