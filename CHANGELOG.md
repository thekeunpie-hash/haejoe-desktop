# Changelog

All notable public releases of **Haejoe Desktop** are documented here.
Install or update at any time via the verified terminal commands in [README.md](README.md) or [https://haejoe.com/local](https://haejoe.com/local).

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

---

## [0.16.779] - 2026-11-18

### Highlights
- **Zero-Electron Desktop Shell (`txiki.js` + WebView2):** Shipped the current production lightweight shell with fast startup, low idle overhead, and native system tray lifecycle management.
- **Verified One-Line Installers:** Published `https://haejoe.com/install.ps1` (Windows PowerShell) and `https://haejoe.com/install.sh` (macOS / Linux) with automatic HTTPS manifest fetch, exact byte-length validation, and SHA-256 verification prior to execution.
- **Public Hub & Integrity Docs:** Launched the upgraded public hub with dark/light adaptive architecture diagrams, zero-touch AI CLI setup prompts, and structured issue templates.

### Improvements
- Improved multi-agent routing and seat quota tracking so parallel runs hand off cleanly when an account approaches its window limit.
- Refined off-screen browser (ABUA) tray behavior and background recovery without stealing desktop focus or cursor control.
- Hardened local credential broker scope enforcement and output redaction across CLI and browser workflows.

---

## [0.16.756] - 2026-11-15

### Added
- **ABUA & ACUA Ambient Runner:** Expanded off-screen browser and background desktop automation primitives with deterministic UI step resolution so user focus remains untouched.
- **Zero-Touch Agent Setup (`/local/setup.txt`):** Added structured `haejoe-local setup plan --json`, `apply`, and `report` flow allowing Claude Code, Codex, and Antigravity to connect MCP servers and workspace instructions automatically.

### Security
- Enforced strict loopback binding (`127.0.0.1:43177`), signed release manifest checks, and OS-backed credential isolation across Windows DPAPI and macOS Keychain.

---

## [0.16.461] - 2026-10-11

### Added
- **Control Desk & Decision Queue:** Unified dashboard showing parallel worker runs, proof-backed completions, multi-account usage meters, and non-blocking owner decision cards.
- **Visual Agent Org Chart:** Role-based delegation hierarchy for lead coordinators, parallel builders, and independent reviewers.
- **Personal Credential Vault UI:** Per-item scope toggles and windowless account brokering for seller portals, AWS, databases, and API tokens.
- **Haejoe Browser Remote (Chrome Extension):** Companion extension on the Chrome Web Store for authenticated browser workflows.

---

> Full release manifests and SHA-256 checksums are served from `https://haejoe.com/api/releases/latest` and displayed on [https://haejoe.com/local](https://haejoe.com/local).
