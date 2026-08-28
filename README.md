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

**Now:** operating the stack below in production and writing up what it actually takes — [Running a fleet of headless coding agents](https://jedarden.com/guides/workflow/) · [/now](https://jedarden.com/now/) · [contact](https://jedarden.com/contact/)

*About the contribution graph:* most of the commits on this profile were landed by that fleet, on these repos. I write the plans, decompose them into tracked units of work, and review the outcomes; the workers do the typing. The guide above explains the loop end to end.

![Repos](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Fusers%2Fjedarden&query=%24.public_repos&label=Projects&style=flat-square&color=2b2b2b&logo=github&logoColor=white)
![Followers](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Fusers%2Fjedarden&query=%24.followers&label=Followers&style=flat-square&color=2b2b2b&logo=github&logoColor=white)

[![Website](https://img.shields.io/badge/jedarden.com-2b2b2b?style=flat-square&logo=google-chrome&logoColor=white)](https://jedarden.com)

[Notes](https://jedarden.com/notes/) · [Guides](https://jedarden.com/guides/) · [Projects](https://jedarden.com/projects/) · [RSS](https://jedarden.com/rss.xml)

`Headless Agentic Development` · `Deterministic State Machines` · `Agent Orchestration` · `Infrastructure Engineering`

</div>

<p align="center">
<a href="#the-headless-agentic-stack">Agentic Stack</a> · <a href="#infrastructure--storage">Infrastructure</a> · <a href="#developer-tooling">Tooling</a>
</p>

---

## The Headless Agentic Stack

Headless agentic development means autonomous agents that claim work from a shared queue, build and test it, and ship through automated pipelines — with humans setting direction and reviewing outcomes rather than driving each task. The system below makes this deterministic: every unit of work has an explicit owner, every outcome has a handler, every deployment is automated. Agents run in parallel across a shared queue, coordinate without colliding, and recover from failures without intervention.

| Tool | Lang | Purpose |
|:-----|:----:|:--------|
| [**NEEDLE**](https://github.com/jedarden/NEEDLE) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | The orchestrator. A deterministic state machine in Rust that processes a shared bead queue, dispatches work to any headless LLM CLI (Claude Code, Codex, Aider), and routes every outcome — success, failure, timeout, crash — through an explicit handler. If an outcome can happen, NEEDLE has a path for it. No implicit fallbacks, no swallowed errors. |
| [**bead-rs**](https://github.com/jedarden/bead-rs) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | Task-coordination store for agent fleets. A dependency graph of "beads" in SQLite; exactly one unblocked bead handed out per request through an atomic single-transaction claim, with a git-tracked checkpoint for lossless recovery. The queue that makes twenty concurrent workers safe. |
| [**HOOP**](https://github.com/jedarden/HOOP) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | Control plane for NEEDLE fleets — launches, tensions, and steers the work across the whole worker pool. |
| [**CLASP**](https://github.com/jedarden/CLASP) | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white) | Drop-in LLM proxy for Claude Code. Swap any OpenAI-compatible provider — Gemini, local models, hosted alternatives — behind Claude Code's interface without touching the orchestration layer. Lets a fleet of NEEDLE workers run on any model mix. |
| [**MANA**](https://github.com/jedarden/MANA) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | Adaptive memory injection for Claude Code. Learns from prior agent sessions and injects relevant context at startup — so each worker begins with accumulated knowledge rather than a blank slate. |
| [**ccdash**](https://github.com/jedarden/ccdash) | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white) | Live TUI dashboard for agent fleet operations: Claude Code token burn rate, system resource load, and tmux session state — all in one terminal pane. Lightweight enough to run alongside a full worker fleet. |
| [**SIGIL**](https://github.com/jedarden/SIGIL) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | Secret injection for AI coding agents — agents use credentials without the values ever entering their context window, closing off prompt-injection exfiltration and transcript leaks. |

---

## Infrastructure & Storage

| Tool | Lang | Purpose |
|:-----|:----:|:--------|
| [**SEAM**](https://github.com/jedarden/SEAM) | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white) | Credential-injecting gateway between the agent fleet and everything it talks to — Kubernetes API across every cluster (read-only observer routes), ArgoCD, OpenBao. Agents and CI call through SEAM; the tokens never leave it. |
| [**ARMOR**](https://github.com/jedarden/ARMOR) | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white) | Encrypted B2 object storage with zero-egress Cloudflare delivery. An S3-compatible, range-readable proxy that encrypts before anything leaves the box and serves through Cloudflare — built after a data-loss incident exposed the risks of egressing plaintext through a public CDN. |

---

## Developer Tooling

| Tool | Lang | Purpose |
|:-----|:----:|:--------|
| [**gribtract**](https://github.com/jedarden/gribtract) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | Pure-Rust GRIB2 decoder — turns NOAA/WMO weather-model output into typed fields and gridded numbers, verified field-by-field against eccodes/wgrib2 over a corpus of real products. No C toolchain, no FFI. |
| [**pdftract**](https://github.com/jedarden/pdftract) | ![Rust](https://img.shields.io/badge/-Rust-000000?style=flat-square&logo=rust&logoColor=white) | PDF text extraction for the cases other tools give up on: reading order, font-encoding recovery, multi-column layouts, and hybrid vector/OCR pipelines, with structured output. |
| [**domain-check**](https://github.com/jedarden/domain-check) | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white) | Authoritative domain availability via RDAP (the ICANN-mandated WHOIS successor) — registry answers, structured JSON, web UI + API. |
| [**agentists-quickstart**](https://github.com/jedarden/agentists-quickstart) | ![Bash](https://img.shields.io/badge/-Shell-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white) | Bootstrap a bare VPS into a working Claude Code + herdr coding environment in one run — the box every worker in the fleet starts from. |

---

## Earlier work

[**duck-e**](https://github.com/jedarden/duck-e) — voice rubber-duck debugging over the OpenAI Realtime API · [**pose-detection**](https://github.com/jedarden/pose-detection) — real-time pose tracking with TensorFlow.js · [**whofi**](https://github.com/jedarden-org/whofi) — what 2.4 GHz WiFi CSI on ESP32 can and cannot do for device-free presence sensing (research notes) · [all projects →](https://jedarden.com/projects/)

---

## Stack

`Rust` · `Go` · `Python` · `TypeScript` · `Kubernetes` · `ArgoCD` · `Argo Workflows` · `Tailscale`
