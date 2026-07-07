<div align="center">

<img width="350" height="350" alt="image" src="https://github.com/user-attachments/assets/9ded9262-6107-42a3-829e-dc4ebe5a6397" />


# BuildAIOS

**Build autonomous AI systems the Linux way.**


[![Runtime Stars](https://img.shields.io/github/stars/buildaios/Runtime-agent?style=flat-square&logo=github&label=Runtime%20Stars&color=FFB000)](https://github.com/buildaios/Runtime-agent/stargazers)

[![Gateway Stars](https://img.shields.io/github/stars/buildaios/MCP-gateway?style=flat-square&logo=github&label=Gateway%20Stars&color=FFB000)](https://github.com/buildaios/MCP-gateway/stargazers)

[![Runtime Contributors](https://img.shields.io/github/contributors/buildaios/Runtime-agent?style=flat-square&label=Runtime%20Contributors&color=0066CC)](https://github.com/buildaios/Runtime-agent/graphs/contributors)

[![Gateway Contributors](https://img.shields.io/github/contributors/buildaios/MCP-gateway?style=flat-square&label=Gateway%20Contributors&color=0066CC)](https://github.com/buildaios/MCP-gateway/graphs/contributors)

[![License](https://img.shields.io/github/license/buildaios/Runtime-agent?style=flat-square)](LICENSE)

[![Built with Podman](https://img.shields.io/badge/Container-Podman-892CA0?style=flat-square&logo=podman&logoColor=white)](https://podman.io)

[![Powered by Fedora](https://img.shields.io/badge/Powered%20by-Fedora-51A2DA?style=flat-square&logo=fedora&logoColor=white)](https://getfedora.org)

<p>
  <a href="#core-philosophy"><b>Philosophy</b></a> •
  <a href="#why-buildaios"><b>Why BuildAIOS?</b></a> •
  <a href="#repositories"><b>Repositories</b></a> •
  <a href="#getting-started"><b>Quick Start</b></a> •
  <a href="https://buildaios.dev"><b>Documentation</b></a>
</p>

<!-- ARCHITECTURE / HERO BANNER -->
<a href="https://buildaios.dev">
  <img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/02289377-033c-4f06-bf7e-9f8a783cd35c" />

</a>

</div>

## What is BuildAIOS?

**BuildAIOS doesn't replace Linux. It teaches Linux how to run AI agents.**

It is a governed AI runtime and control plane that turns Fedora Linux into a secure orchestration environment for autonomous workflows. 

Instead of reinventing scheduling, logging, and security in user-space Python or Node.js frameworks, BuildAIOS maps AI agent requirements directly to native OS primitives. By combining `systemd`, `Podman`, `SELinux`, and the Model Context Protocol (MCP) under a unified control plane, you get the flexibility of modern AI agents with the deterministic, robust execution of native system processes.

## Why BuildAIOS?

Why use an OS-level runtime instead of an application-layer framework like LangGraph, OpenHands, or Claude Code?

| Traditional Agent Framework | BuildAIOS |
| :--- | :--- |
| **User-space runtime** | **Native Linux runtime** (`systemd`-managed) |
| **Custom application sandbox** | **Strict kernel isolation** (`SELinux` + `Podman`) |
| **Custom while-loop scheduler** | **Battle-tested OS scheduler** (`systemd` timers & targets) |
| **Proprietary framework logs** | **Tamper-resistant system logs** (`journald`) |
| **Manual script orchestration**| **Policy-driven control plane** (`Polkit` governance) |

---

## Core Philosophy

Our architectural thesis is simple: **Borrow Infrastructure. Build Governance.** 

| Linux Primitives | | BuildAIOS Capabilities |
| :--- | :---: | :--- |
| **`systemd`** | ➔ | **Workflow Runtime** (Lifecycle & process management) |
| **`Podman`** | ➔ | **Agent Runtime** (Secure, rootless container isolation) |
| **`SELinux`** | ➔ | **Trust Engine** (Mandatory access control for models & tools) |
| **`Polkit`** | ➔ | **Human Approval** (Privilege escalation & manual gates) |
| **`Git`** | ➔ | **Recovery Engine** (State versioning & rollback capability) |
| **`Journald`** | ➔ | **Audit Layer** (Structured, tamper-resistant system logs) |
| **`OCI Images`** | ➔ | **Environment Packs** (Standardized, distributable agent runtimes) |
| **`MCP`** | ➔ | **Gateway Governance** (Secure, unified tool & context access) |

---

## The BuildAIOS Experience

<table width="100%" style="border: none; border-collapse: collapse;">
  <tr>
    <td width="33%" align="center" style="border: none; padding: 10px;">
      <b>CLI Control Plane</b><br>
      <img src="https://raw.githubusercontent.com/buildaios/.github/main/profile/assets/preview-cli.png" alt="BuildAIOS CLI" width="100%" style="border-radius: 6px; margin-top: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"/>
    </td>
    <td width="33%" align="center" style="border: none; padding: 10px;">
      <b>MCP Gateway Dashboard</b><br>
      <img src="https://raw.githubusercontent.com/buildaios/.github/main/profile/assets/preview-gateway.png" alt="BuildAIOS Gateway" width="100%" style="border-radius: 6px; margin-top: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"/>
    </td>
    <td width="33%" align="center" style="border: none; padding: 10px;">
      <b>Desktop Approval UI</b><br>
      <img src="https://raw.githubusercontent.com/buildaios/.github/main/profile/assets/preview-desktop.png" alt="BuildAIOS Desktop UI" width="100%" style="border-radius: 6px; margin-top: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);"/>
    </td>
  </tr>
</table>

---

## Core Features

<table width="100%" style="border-collapse: collapse; border: none;">
  <tr style="border: none; background: transparent;">
    <td width="50%" style="border: none; padding: 16px; vertical-align: top;">
      <h3>🛡️ Governed Execution</h3>
      <p>Prevent unauthorized API calls, file access, and model interactions before they happen via strict SELinux-style boundary policies and Polkit manual approval gates.</p>
    </td>
    <td width="50%" style="border: none; padding: 16px; vertical-align: top;">
      <h3>⚙️ Recoverable Runtime</h3>
      <p>If an agent is OOM-killed or the host system restarts, BuildAIOS resumes execution precisely where it left off using state-hydrated workflows and Git-backed memory.</p>
    </td>
  </tr>
  <tr style="border: none; background: transparent;">
    <td width="50%" style="border: none; padding: 16px; vertical-align: top;">
      <h3>🌐 Native MCP Gateway</h3>
      <p>Safely expose enterprise data sources, local files, and web APIs to both local and remote models through a secure Model Context Protocol proxy.</p>
    </td>
    <td width="50%" style="border: none; padding: 16px; vertical-align: top;">
      <h3>📦 Environment Packs</h3>
      <p>Run specialized agents inside immutable OCI-compliant Podman containers, completely isolating their dependencies, languages, and toolchains.</p>
    </td>
  </tr>
</table>

---

## System Architecture

<div align="center" style="margin: 30px 0;">
  <a href="https://buildaios.dev/docs/architecture">
    <img src="https://raw.githubusercontent.com/buildaios/.github/main/profile/assets/architecture-diagram.svg" alt="BuildAIOS Layered Architecture" width="100%" style="max-width: 850px; border-radius: 6px; box-shadow: 0 4px 12px rgba(0,0,0,0.1);"/>
  </a>
</div>

*For a detailed breakdown of the 7-layer OS routing stack, read the [Architecture Design Records](https://buildaios.dev/docs/architecture).*

---

## Current Focus

We build in the open. Here is what the core team is currently focused on:

```text
✓ Runtime engine & systemd scheduling
✓ MCP Gateway & core tool routing
• Environment Packs (OCI isolation)
• Memory Layer (Git-backed state)
• Desktop GUI (Polkit agent)
```

---

## Repositories

BuildAIOS is modular by design. Our core systems are split into the following repositories:

| Repository | Purpose | Status |
| :--- | :--- | :---: |
| [**`runtime`**](https://github.com/buildaios/runtime) | Core agent execution, `systemd` process mapping, and Podman | 🟢 Active |
| [**`gateway`**](https://github.com/buildaios/gateway) | Secure MCP proxy, rate limiting, and policy enforcement layer | 🟢 Active |
| [**`docs`**](https://github.com/buildaios/docs) | Architecture Decision Records (ADRs), guides, and topology | 🟢 Active |
| [**`website`**](https://github.com/buildaios/website) | Public landing page and documentation portal front-end | 🟡 Beta |
| [**`.github`**](https://github.com/buildaios/.github) | Global organization profiles, issue templates, and CI/CD | 🟢 Active |

---

## 🗺️ Roadmap

* **Phase 1: Foundation** — Stable `systemd`-backed runtime engine, local MCP tool routing, and rootless Podman agent isolation.
* **Phase 2: Core Runtime** — Distributed DAG workflow scheduler, `Polkit` human-in-the-loop approval gates, and signed `journald` audit logs.
* **Phase 3: Desktop Integration** — Lightweight local UI management dashboard, system tray monitoring, and guided agent bootstrapping.
* **Phase 4: Distributed & Edge** — Decentralized Environment Pack marketplace and multi-node cluster orchestration.

---

## Getting Started

Ready to run governed agents on Linux?

* [**Quick Start Guide**](https://buildaios.dev/docs/getting-started) — Spin up your first governed agent in under 5 minutes.
* [**MCP Gateway Setup**](https://buildaios.dev/docs/mcp) — Connect your local LLMs to system tools securely.
* [**Building Environment Packs**](https://buildaios.dev/docs/packs) — Create isolated runtime environments for specialized workloads.

---

## Contribute

We are building the open standard for AI orchestration on Linux, and we welcome contributions from system architects, OS engineers, and AI developers.

* **[Good First Issues](https://github.com/buildaios/runtime/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)** — Find an easy entry point into the codebase.
* **[Discussions & RFCs](https://github.com/orgs/buildaios/discussions)** — Join active design proposals and technical debates.
* **[Discord](https://discord.gg/buildaios)** — Chat with the core maintainers.

---

<p align="center">
  <b>Built natively on Fedora Linux. Released under the MIT License.</b><br>
  <img src="https://raw.githubusercontent.com/buildaios/.github/main/profile/assets/fedora-logo-small.svg" alt="Fedora OS" width="24" style="margin-top: 12px;"/>
</p>
