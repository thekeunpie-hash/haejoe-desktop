# Security Policy

Haejoe Desktop is built on a single principle: **delegation without exposure**. Your credentials, local repositories, and desktop session stay on your machine, and AI agents operate strictly inside the boundaries you approve.

---

## Supported Versions

| Version | Supported | Notes |
| :--- | :--- | :--- |
| `0.16.779` (Latest) | Yes | Active production release with verified SHA-256 manifest |
| `>= 0.16.60` | Security fixes | Minimum baseline security version; update recommended |
| `< 0.16.60` | No | Unsupported; upgrade via `install.ps1` or `install.sh` |

---

## Local Vault Architecture (Windows DPAPI & macOS Keychain)

Haejoe Desktop never stores plaintext secrets in prompt templates, workspace dotfiles, or remote servers.

1. **OS-Backed Encryption at Rest**
   - **Windows 10 / 11:** Secrets are sealed using the Windows Data Protection API (DPAPI), bound to your local OS user context.
   - **macOS:** Secrets are stored inside the native macOS Keychain.
   - Seller logins, AWS keys, SSH keys, database credentials, and API tokens stay on your own PC.

2. **Opaque Handle Brokering (Zero LLM Exposure)**
   - Connected agents (Claude Code, Codex, Antigravity, Cursor, Devin, Web AI connectors) receive only non-sensitive metadata and opaque credential handles (`cred_…`).
   - When an agent triggers a permitted action (`haejoe-local credential exec`, scoped HTTP, AWS SigV4, database query, or off-screen ABUA sign-in), the local broker resolves the credential strictly in-memory at the execution boundary.
   - Before returning command output or logs to an agent, the output scrubber redacts tokens, session headers, and cookie values.

3. **Loopback Control Plane & Owner Approval Boundary**
   - The local control server binds to loopback (`127.0.0.1:43177`).
   - Workspace folder scope, external domain allowlists, and credential permissions are granted explicitly by the PC owner and can be revoked in one click.
   - Off-screen browser automation (ABUA) runs in an isolated agent browser profile and never accesses your personal Chrome profile or active desktop focus without opt-in.

---

## Release Integrity & SHA-256 Verification

Every official installation script (`https://haejoe.com/install.ps1` and `https://haejoe.com/install.sh`) automatically enforces HTTPS-only download transport, exact byte-length verification, and SHA-256 digest matching before executing anything.

You can also inspect and verify the live release manifest yourself at any time:

### Windows (PowerShell)

```powershell
# 1. Inspect the official release manifest over HTTPS
$manifest = Invoke-RestMethod -Uri "https://haejoe.com/api/releases/latest?os=win32&arch=x64"
$manifest | Select-Object version, sizeBytes, sha256, publishedAt

# 2. Verify any locally downloaded installer file before running it
(Get-FileHash -Path "<path-to-downloaded-installer>" -Algorithm SHA256).Hash.ToLowerInvariant() -eq $manifest.sha256.ToLowerInvariant()
```

### macOS / Linux (Terminal)

```bash
# 1. Inspect the official release manifest over HTTPS (use os=darwin or os=linux, arch=arm64 or arch=x64)
curl -fsSL "https://haejoe.com/api/releases/latest?os=$(uname -s | tr '[:upper:]' '[:lower:]')&arch=$(uname -m | sed 's/x86_64/x64/;s/aarch64/arm64/')"

# 2. Compare against your downloaded payload
shasum -a 256 "<path-to-downloaded-package>"
# or on Linux:
sha256sum "<path-to-downloaded-package>"
```

### Unsigned Windows Installer Notice

Authenticode code-signing enrollment is currently underway. Until code signing is active, Windows SmartScreen may display an unrecognized-publisher warning on first launch. Always confirm the SHA-256 digest matches the official manifest published on [https://haejoe.com/local](https://haejoe.com/local) before selecting **More info → Run anyway**.

---

## Reporting a Vulnerability

If you discover a security issue in Haejoe Desktop, the local credential broker, the installer scripts, or the `haejoe.com/local` release pipeline, please report it privately so we can investigate and ship a fix promptly.

- **Email:** `admin@haejoe.com` (subject prefix: `[Security] Haejoe Desktop`)
- **Do not open a public GitHub issue** for undisclosed security vulnerabilities.

### What to Include

- Haejoe Desktop version and OS / architecture (`Windows 11 x64`, `macOS arm64`, etc.)
- Clear steps to reproduce the issue and affected component (Vault, MCP bridge, ABUA browser, installer)
- Potential impact and any suggested remediation
- **Never attach real passwords, API keys, session cookies, or private credentials**

### Response Targets

- **Initial acknowledgement:** Within 48 hours
- **Triage and remediation plan:** Within 5 business days
- **Coordinated disclosure:** We will credit reporters (upon request) in `CHANGELOG.md` once a fix is published.
