# Netvatic Release Verification

All binaries published in releases of this repository are signed with one of two
hardware-backed GPG keys held by Bionic Technologies Ltd. **Verify every download
before running it.** A binary that does not verify against one of the trusted
keys below is not an authentic Netvatic release, and customer agents will refuse
to install it.

## Trusted signing keys

> **Status:** placeholder — keys not yet generated. The fingerprints below will
> be populated after the release-signing ceremony per
> [docs/security/RELEASE_SIGNING_RUNBOOK.md](https://github.com/boywiz/netvatic/blob/master/docs/security/RELEASE_SIGNING_RUNBOOK.md)
> in the Netvatic source repo. Do not trust any release in this repository until
> this notice is removed and the table below is populated.

| Role | Fingerprint | UID | Algorithm |
|---|---|---|---|
| Primary | `TBD (40-char hex)` | `Bionic Technologies (Netvatic Release Signing) <releases@netvatic.com>` | Ed25519 |
| Backup  | `TBD (40-char hex)` | `Bionic Technologies (Netvatic Release Signing Backup) <releases@netvatic.com>` | RSA-2048 |

Public key files will be published at:
- [`netvatic-release-pubkey-primary.asc`](./netvatic-release-pubkey-primary.asc)
- [`netvatic-release-pubkey-backup.asc`](./netvatic-release-pubkey-backup.asc)

## Verifying a downloaded binary

```bash
# 1. Download the binary + the SHA256SUMS file + its signature
gh release download vX.Y.Z --repo bionic-tech/netvatic-releases

# 2. Import both public keys (once)
gpg --import netvatic-release-pubkey-primary.asc netvatic-release-pubkey-backup.asc

# 3. Verify the signature against the SHA256SUMS file
gpg --verify SHA256SUMS.asc SHA256SUMS

# 4. Verify the binaries against the (now-trusted) SHA256SUMS
sha256sum -c SHA256SUMS
```

Step 3 MUST output **`Good signature from "Bionic Technologies ..."`** with one
of the two fingerprints listed above. If you see `BAD signature`, `No public
key`, or a fingerprint mismatch, **do not run the binary** and report the
incident at the address below.

## Hardware custody

The signing keys exist only on hardware tokens (YubiKey 5C NFC for the primary,
YubiKey NEO for the backup). They cannot be exfiltrated, copied, or used
remotely. A revocation certificate is stored offline across two physically
separated USB drives; in the event of catastrophic key loss, the revocation
will be published here.

## Reporting a security issue

If you have found a vulnerability in Netvatic or have reason to believe a
release here was published without authorisation, email
**security@netvatic.com** with a detailed report. Please do not open a public
GitHub issue for security concerns.

We aim to acknowledge security reports within 2 working days.

## What lives in this repository

This repository holds **only** the public Remote Site Agent binary, signing
material, and verification metadata. The Netvatic orchestrator container image,
helm charts, Docker Compose files, and Terraform modules are distributed
separately — see [https://netvatic.com](https://netvatic.com) for access.

Source code is not published here. The agent's source license model is under
review (Apache 2.0 vs BSL); until that decision is recorded, all rights are
reserved by Bionic Technologies Ltd.
