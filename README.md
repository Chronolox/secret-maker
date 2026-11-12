<div align="center">

<a href="https://chronolox.com">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/chronolox-logo-dark.png">
    <img src="assets/chronolox-logo-light.png" alt="Chronolox — hourglass emblem and wordmark" width="360">
  </picture>
</a>

</div>

# Secret Maker — Desktop Creator Application

This repository hosts official, pre-compiled desktop application releases, installer packages, release signatures, and integrity verification materials for **Secret Maker** (`secret-maker`).

Secret Maker is the desktop creator application for local secret authoring, multi-layer capsule packaging (`.clox`), life-planning template entry, and time-locked vault publication.

Pre-built binaries, desktop installers (`.deb`, `.msix`), and application bundles are available on the [Releases](https://github.com/Chronolox/secret-maker/releases) page.

---

## Capabilities

- **Desktop Vault Authoring:** Guided local authoring of time-locked archives and secret instructions.
- **Autonomous Capsule Packaging:** Packages files, life-planning templates, and multimedia assets into Reed-Solomon protected `.clox` capsules.
- **Physical USB Burner & Redundancy Pool:** Write bootable or data-only USB keys with automatic parity verification and volume branding.
- **On-Chain Vault Publication:** Seal and register vaults on-chain with zero-knowledge recipient certificates.

---

## Release Verification Keys

All official binaries are cryptographically signed before release. Never execute binaries whose SHA-256 digests or GPG signatures do not match the published records.

### Public Signing Keys

- **Release Signing GPG Key ID:** `0xF873EA8F770A9136`
- **Key Fingerprint:** `CE23 439F 2EA0 9A0C 445A  F720 F873 EA8F 770A 9136`
- **User ID:** `Chronolox APT Signing Key <apt@chronolox.com>`
- **Public Key File:** Included in repository root as [`chronolox-release-key.pub`](./chronolox-release-key.pub) — always verify the fingerprint above after importing; trust the fingerprint, not the transport.

Import the key and verify a release:

```bash
gpg --import chronolox-release-key.pub
gpg --fingerprint 0xF873EA8F770A9136          # must match the fingerprint above
gpg --verify SHA256SUMS.sig SHA256SUMS        # against a release's checksum ledger
sha256sum --check SHA256SUMS --ignore-missing
```

---

## Integrity & Authenticity Verification

Each release on GitHub includes:

1. The platform binary installer / archive (`.deb`, `.tar.gz`, `.zip`, `.msix`)
2. `SHA256SUMS` (Plaintext hash ledger)
3. `SHA256SUMS.sig` (Detached GPG signature of the hash ledger)

### 1. Verify Checksum Ledger Signature

Verify that the checksum ledger itself has not been tampered with:

```bash
gpg --verify SHA256SUMS.sig SHA256SUMS
```

*Expected output:* `gpg: Good signature from "Chronolox APT Signing Key <apt@chronolox.com>"`

### 2. Verify Binary Integrity

Run the checksum check against your downloaded archive:

#### Linux / macOS

```bash
sha256sum --check SHA256SUMS --ignore-missing
```

#### Windows (PowerShell)

```powershell
Get-FileHash -Algorithm SHA256 .\secret-maker-windows-amd64.zip
# Compare output manually against SHA256SUMS entry
```

---

## Installation & Execution Notes

### Linux (`amd64` / `arm64`)

```bash
# Direct archive extraction
tar -xzf secret-maker-linux-amd64.tar.gz
./secret-maker
```

> **Debian / Ubuntu Package:** Native `.deb` packages can be installed via:
> ```bash
> sudo apt install ./secret-maker_*_amd64.deb
> ```

### macOS (`arm64` / Apple Silicon)

Extract the `.zip` archive containing the notarized `Secret Maker.app` bundle:

```bash
unzip secret-maker-darwin-arm64.zip
xattr -d com.apple.quarantine "Secret Maker.app"
open "Secret Maker.app"
```

### Windows (`amd64`)

- **MSIX Package:** Double-click the `.msix` bundle to install via Windows App Installer.
- **Standalone Zip:** Extract `secret-maker-windows-amd64.zip` and run `secret-maker.exe`.

---

## Security & Bug Reporting

If you observe a checksum mismatch, corrupted binary artifact, or unexpected network behavior:

* **Do NOT file a public issue or pull request for security vulnerabilities.**
* Review our disclosure procedure in [`SECURITY.md`](./SECURITY.md).
* Contact our engineering security desk directly at **`security@chronolox.com`**.

---

## Contributing

To report packaging bugs, operating system compatibility issues, or hash verification errors, please see [`CONTRIBUTING.md`](./CONTRIBUTING.md).

---

## License

The binary releases and verification materials in this repository are distributed under the [Chronolox Binary Release License](./LICENSE).

Source code for the underlying applications is protected during commercial beta by the on-chain Cryptographic Source Escrow Failsafe documented in [`specs`](https://github.com/Chronolox/specs).
