# Netvatic Releases

Public release distribution for **Netvatic** — agent binaries and signed
verification material.

This repository contains:

- Signed builds of the **Netvatic Remote Site Agent** — a small outbound-only
  binary that performs local network discovery (SNMP, SSH, SDN, container,
  cloud, zero-trust) at a customer site and ships encrypted results to a
  central Netvatic orchestrator over mTLS.
- The signing-key fingerprints and verification instructions —
  see [SECURITY.md](./SECURITY.md).

Source code, the orchestrator container image, Helm charts, Docker Compose
files, and Terraform modules are distributed separately.
See [netvatic.com](https://netvatic.com) for access.

## Downloading the agent

Latest release: see the [Releases page](https://github.com/bionic-tech/netvatic-releases/releases/latest).

Available builds:

- `netvatic-agent-vX.Y.Z-linux-amd64.tar.gz` (Linux x86-64)
- Additional platforms added as the product matures.

## Verifying a download

**Verify every download.** A binary that does not verify against one of the
trusted signing keys in [SECURITY.md](./SECURITY.md) is not an authentic
Netvatic release, and Netvatic customer agents will refuse to install it.

```bash
# Pull the release into the current directory
gh release download vX.Y.Z --repo bionic-tech/netvatic-releases

# Import the signing public keys (once)
gpg --import netvatic-release-pubkey-primary.asc netvatic-release-pubkey-backup.asc

# Verify the SHA256SUMS file is genuine
gpg --verify SHA256SUMS.asc SHA256SUMS

# Verify the binaries against the now-trusted SHA256SUMS
sha256sum -c SHA256SUMS
```

Full verification protocol and signing-key custody documentation in
[SECURITY.md](./SECURITY.md).

## Reporting issues

- **Security issues:** email `security@netvatic.com` — do not open a public
  GitHub issue.
- **Bug reports and feature requests** for the agent: use the Netvatic
  customer portal at `portal.netvatic.com`.

## About Bionic Technologies

Netvatic is a product of Bionic Technologies Ltd, a UK-registered company.
