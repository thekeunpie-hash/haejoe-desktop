# Haejoe Desktop

[한국어](README.ko.md)

Haejoe Desktop runs the AI coding agents you already use, several at a time, in the background of your own PC.
They work off-screen, so your mouse, keyboard and windows stay yours while they run.

**Download:** https://haejoe.com/local

This repository holds the public notes and release announcements. The app's source code is not published here.

## What it does

- **Connects the agents you already have.** Claude Code, Codex, Antigravity, Devin, Cursor, VS Code, Gemini CLI,
  Claude, ChatGPT and Gemini. One auto-connect ties them to a work folder on your PC. Each service's own plan and
  limits still apply.
- **Runs them side by side, off-screen.** Work is split across the connected agents and runs in the background. The
  app does not take your focus or move your mouse.
- **Keeps your keys in a vault on your PC.** Account passwords and API keys (seller accounts, AWS, databases, API
  keys) stay in the operating system's encrypted store (Windows DPAPI, macOS Keychain). Agents ask the app to use
  them within the scope you allow; they never see the raw values.
- **Uses what is already installed.** It works with the official Chrome and Codex already on your PC instead of
  shipping its own copies.

## Requirements

- Windows 10/11 (installer). macOS and iOS/iPadOS connect through the local bridge, the MCP connector and the
  Chrome extension.
- An account on at least one of the AI services above.

## Installing

The Windows installer is not code-signed yet, so SmartScreen may warn on first run. Choose **More info → Run
anyway**. You can check that the file is the published one on the download page.

## Releases

Each release on this page links to the matching build on https://haejoe.com/local together with its notes.

## Links

- Product page: https://haejoe.com/local
- Haejoe (development outsourcing with escrow): https://haejoe.com
