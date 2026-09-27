---
title: 'Full-Disk Encryption'
description: 'What FDE does and does not protect against, and how to set it up without losing the recovery key.'
category: 'operating-systems'
difficulty: 'introductory'
added: '2026-09-27'
updated: '2026-09-27'
author: 'Archive-Opsec contributors'
tags: ['encryption', 'key-management', 'hardware']
status: 'published'
sources:
  - title: 'NIST SP 800-111: Guide to Storage Encryption Technologies for End User Devices'
    url: 'https://csrc.nist.gov/pubs/sp/800/111/final'
    publisher: 'National Institute of Standards and Technology'
    kind: 'standards'
    accessed: '2026-09-27'
  - title: 'LUKS2 On-Disk Format Specification'
    url: 'https://gitlab.com/cryptsetup/cryptsetup/-/raw/main/docs/on-disk-format-luks2.pdf'
    publisher: 'The cryptsetup project'
    kind: 'standards'
    note: 'The on-disk format specification, maintained by the cryptsetup project. This is not an IETF standard and never was: an earlier citation to draft-camara-hw-encrypted-luks pointed at a draft that was never published.'
    accessed: '2026-09-27'
  - title: 'About BitLocker'
    url: 'https://learn.microsoft.com/en-us/windows/security/operating-system-security/data-protection/bitlocker/'
    publisher: 'Microsoft Corporation'
    kind: 'documentation'
    accessed: '2026-09-27'
  - title: 'FileVault and other security protections for a Mac'
    url: 'https://support.apple.com/guide/security/filevault-and-other-security-protections-sec46bda94ec7/web'
    publisher: 'Apple Inc.'
    kind: 'documentation'
    accessed: '2026-09-27'
related:
  guides:
    [
      'operating-systems/hardening-basics',
      'encryption/encryption-explained',
      'encryption/key-management',
      'mobile/mobile-device-privacy',
    ]
  archive: []
  news: []
---

Full-disk encryption encodes the entire contents of a storage device and only decrypts it
once the correct key is presented. On a powered-off or locked device, the contents are
unreadable. It is the single most effective control against device loss and theft.

## What it protects against

- **A stolen, powered-off laptop.** The disk contents are ciphertext.
- **A stolen, powered-on but locked device**, provided the key is held in hardware.
- **Recovery of files from a discarded or resold drive**, which is the case most often
  forgotten.
- **Untargeted disk-imaging attacks**, where an adversary pulls the drive and processes it
  offline at leisure.

## What it does not protect against

:::warning

- **An unlocked session.** Anyone with the device and your credentials can read everything.
  Encryption protects data at rest.
- **An attacker with your account.** Signing in defeats it entirely.
- **Someone who can observe the screen or capture keystrokes.**
- **A hostile administrator of the device while it is running.** This is why
  [hardening](/guides/hardening-basics/) exists alongside encryption.
- **A weak master password.** The disk is only as strong as the passphrase protecting the
  key.
  :::

## Where the key lives

| Approach      | How the key is released                                                        | Trade-off                                                                       |
| ------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| TPM-backed    | The platform's secure hardware releases the key after verifying boot integrity | Best balance: no password at boot, and it does not release to a modified system |
| TPM plus PIN  | As above, with a second factor you must enter at boot                          | Resists someone who removes the drive and puts it in another machine            |
| Password only | The passphrase decrypts the key directly                                       | Portable between machines; protected only by the passphrase                     |

:::note
The TPM option is the one to prefer on a laptop, and "TPM plus PIN" if the threat model
includes physical possession of the device by someone who knows your login password.
Modern hardware makes this unobtrusive: the boot is usually transparent.
:::

## Setting it up

**Windows — BitLocker.** The device must have TPM 2.0 and secure boot. Save the recovery
key, and decide deliberately whether to also require a PIN.

**macOS — FileVault.** Enable from System Settings; the recovery key is escrowed to an
Apple account only if you choose that.

**Linux — LUKS.** Straightforward and fully under your control:

```bash
# Encrypt a new partition during installation, or afterwards
cryptsetup luksFormat --type luks2 /dev/nvme0n1p3
cryptsetup open /dev/nvme0n1p3 luks_crypt
mkfs.ext4 /dev/mapper/luks_crypt
```

With a header and keyfile for a machine you manage yourself:

```bash
# 1. Create the encrypted container
cryptsetup luksFormat --type luks2 --cipher aes-xts-plain64 --key-size 512 /dev/sdb1

# 2. Back up the header. If this volume's header is lost, the data is unrecoverable.
cryptsetup luksHeaderBackup /dev/sdb1 --header-backup-file luks-header-backup.bin

# 3. Create and open it
cryptsetup open --type luks2 /dev/sdb1 crypt_archive
mkfs.xfs /dev/mapper/crypt_archive
```

A very large LUKS2 header with additional integrity protection is worth considering for
long-lived archives:

```bash
cryptsetup luksFormat --type luks2 \
  --integrity hmac-sha256 \
  --key-size 512 \
  --cipher aes-xts-plain64 \
  /dev/sdb1
```

:::warning
Always back up the LUKS header. It is small, it is easy to store, and without it the data
is permanently inaccessible even with the correct passphrase.
:::

## Do not forget

1. Store the recovery key in a password manager and, ideally, printed somewhere separate
   from the device.
2. Store the LUKS header backup separately from the drive it unlocks.
3. Verify the recovery path once: restore from the recovery key, or unlock the header
   backup on a different machine.
4. If the device is reinstalled, a new encryption setup is not automatically a continuation
   of the old one. Check what you expect to still be readable.

## Sources

- [NIST SP 800-111](https://csrc.nist.gov/pubs/sp/800/111/final) — storage encryption
  for end-user devices, including pre-boot authentication and the threat model.
- [LUKS specification](https://gitlab.com/cryptsetup/cryptsetup/-/raw/main/docs/on-disk-format-luks2.pdf)
  — the on-disk format, key slots, and integrity options.
- [Microsoft: About BitLocker](https://learn.microsoft.com/en-us/windows/security/operating-system-security/data-protection/bitlocker/)
  — device requirements and the TPM model.
- [Apple: FileVault](https://support.apple.com/guide/security/filevault-and-other-security-protections-sec46bda94ec7/web)
  — the platform description, including what it protects against on a Mac.
