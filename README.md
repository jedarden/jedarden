![](banner.png)

<div align="center">

# Jed Arden

**New York** · Agentic Systems Engineer

![Rust](https://img.shields.io/badge/-Rust-2b2b2b?style=flat-square&logo=rust&logoColor=dea584)
![Go](https://img.shields.io/badge/-Go-2b2b2b?style=flat-square&logo=go&logoColor=00ADD8)
![Python](https://img.shields.io/badge/-Python-2b2b2b?style=flat-square&logo=python&logoColor=3776AB)
![TypeScript](https://img.shields.io/badge/-TypeScript-2b2b2b?style=flat-square&logo=typescript&logoColor=3178C6)
![Kubernetes](https://img.shields.io/badge/-Kubernetes-2b2b2b?style=flat-square&logo=kubernetes&logoColor=326CE5)
![Claude](https://img.shields.io/badge/-Claude-2b2b2b?style=flat-square&logo=anthropic&logoColor=d4a27f)

*I build headless agent orchestration, cloud-native infrastructure, and the systems that make autonomous work safe to ship.*

![Stars](https://img.shields.io/badge/Stars-327+-2b2b2b?style=flat-square&logo=github&logoColor=white)
![Repos](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Fusers%2Fjedarden&query=%24.public_repos&label=Projects&style=flat-square&color=2b2b2b&logo=github&logoColor=white)
![Contributions](https://img.shields.io/badge/Contributions_(1yr)-54%2C626-2b2b2b?style=flat-square&logo=github&logoColor=white)
![Followers](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Fusers%2Fjedarden&query=%24.followers&label=Followers&style=flat-square&color=2b2b2b&logo=github&logoColor=white)

[![Website](https://img.shields.io/badge/jedarden.com-2b2b2b?style=flat-square&logo=google-chrome&logoColor=white)](https://jedarden.com)

`Headless Agentic Development` · `Deterministic State Machines` · `Agent Orchestration` · `Infrastructure Engineering`

</div>

<p align="center">
<a href="#the-headless-agentic-stack">Agentic Stack</a> · <a href="#infrastructure--storage">Infrastructure</a> · <a href="#developer-tooling">Tooling</a>
</p>

---

## The Headless Agentic Stack

Headless agentic development means autonomous agents that claim work from a shared queue, build and test it, and ship through automated pipelines — with humans setting direction and reviewing outcomes rather than driving each task. The system below makes this deterministic: every unit of work has an explicit owner, every outcome has a handler, every deployment is automated. Agents run in parallel across a shared queue, coordinate without colliding, and recover from failures without intervention.

| Tool | Stars | Lang | Purpose |
|:-----|:-----:|:----:|:--------|
| [**NEEDLE**](https://github.com/jedarden/NEEDLE) | ![Stars](https://img.shields.io/github/stars/jedarden/NEEDLE?style=flat-square&label=⭐) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | The orchestrator. A deterministic state machine in Rust that processes a shared bead queue, dispatches work to any headless LLM CLI (Claude Code, Codex, Aider), and routes every outcome — success, failure, timeout, crash — through an explicit handler. If an outcome can happen, NEEDLE has a path for it. No implicit fallbacks, no swallowed errors. |
| [**HOOP**](https://github.com/jedarden/HOOP) | ![Stars](https://img.shields.io/github/stars/jedarden/HOOP?style=flat-square&label=⭐) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | Control plane for NEEDLE fleets — launches, tensions, and steers the work across the whole worker pool. |
| [**CLASP**](https://github.com/jedarden/CLASP) | ![Stars](https://img.shields.io/github/stars/jedarden/CLASP?style=flat-square&label=⭐) | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white) | Drop-in LLM proxy for Claude Code. Swap any OpenAI-compatible provider — Gemini, local models, hosted alternatives — behind Claude Code's interface without touching the orchestration layer. Lets a fleet of NEEDLE workers run on any model mix. |
| [**MANA**](https://github.com/jedarden/MANA) | ![Stars](https://img.shields.io/github/stars/jedarden/MANA?style=flat-square&label=⭐) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | Adaptive memory injection for Claude Code. Learns from prior agent sessions and injects relevant context at startup — so each worker begins with accumulated knowledge rather than a blank slate. |
| [**ccdash**](https://github.com/jedarden/ccdash) | ![Stars](https://img.shields.io/github/stars/jedarden/ccdash?style=flat-square&label=⭐) | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white) | Live TUI dashboard for agent fleet operations: Claude Code token burn rate, system resource load, and tmux session state — all in one terminal pane. Lightweight enough to run alongside a full worker fleet. |

---

## Infrastructure & Storage

| Tool | Stars | Lang | Purpose |
|:-----|:-----:|:----:|:--------|
| [**ARMOR**](https://github.com/jedarden/ARMOR) | ![Stars](https://img.shields.io/github/stars/jedarden/ARMOR?style=flat-square&label=⭐) | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white) | Encrypted B2 object storage with zero-egress Cloudflare delivery. An authenticated, range-readable proxy that keeps backup data encrypted end-to-end — built after a data loss incident exposed the risks of egressing plaintext through a public CDN. Production-hardened. |

---

## Developer Tooling

| Tool | Stars | Lang | Purpose |
|:-----|:-----:|:----:|:--------|
| [**agentists-quickstart**](https://github.com/jedarden/agentists-quickstart) | ![Stars](https://img.shields.io/github/stars/jedarden/agentists-quickstart?style=flat-square&label=⭐) | ![Bash](https://img.shields.io/badge/-Shell-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white) | Opinionated DevPod workspace configs for agentic engineering. Shared secrets from GitHub Codespaces or 1Password, curated extensions, and pre-configured environments — basic and security-focused — ready on first launch. The fastest path from zero to a working agentic dev environment. |

---

## Stack

`Rust` · `Go` · `Python` · `TypeScript` · `Kubernetes` · `ArgoCD` · `Argo Workflows` · `Tailscale`
