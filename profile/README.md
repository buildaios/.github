# BuildAIOS

[![Project Status: Active Dev](https://img.shields.io/badge/Project%20Status-Active--Dev-blueviolet.svg)](#)
[![Host OS: Fedora Linux](https://img.shields.io/badge/Host%20OS-Fedora%20Linux-blue.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#)

BuildAIOS is a governed, recoverable AI operating system and cognitive control plane engineered directly above Fedora Linux. Designed to execute high-autonomy agent workflows, consolidate deep context assets, orchestrate rootless containment wrappers, and link unified inference pipelines—all under high-grade kernel containment boundaries.

The core engineering paradigm represents a radical shift from standard, userspace-only agent loops: **"Borrow Infrastructure, Build Governance."** Instead of recreating core system utilities, BuildAIOS implements state-of-the-art orchestration layers that interface directly with battle-tested Linux system APIs.

---

## Technical Overview
```
                         ┌─────────────────────────────────────────────────────────────┐
                         │           Desktop Workspace (Wayland / Web Portals)         │
                         └──────────────────────────────┬──────────────────────────────┘
                                                        │ D-Bus Control Loop
                                                        ▼
                         ┌─────────────────────────────────────────────────────────────┐
                         │              systemd (cgroups v2 Control Engine)            │
                         └──────┬───────────────────────────────────────────────┬──────┘
                                │                                               │
                                ▼                                               ▼
     ┌─────────────────────────────────────────────────────┐ ┌───────────────────────────────────────┐
     │          Inference Host Services (vLLM / Ollama)     │ │     Transient systemd-run --user      │
     └─────────────────────────────────────────────────────┘ └──────────────────┬────────────────────┘
                                                                                │ Namespace Isolation
                                                                                ▼
                                                             ┌───────────────────────────────────────┐
                                                             │     Rootless Podman Container Space   │
                                                             └───┬───────────────────────────────┬───┘
                                                                 │                               │
                                                                 ▼                               ▼
                                                   ┌──────────────────────────┐    ┌──────────────────────────┐
                                                   │    Agent Process Loop    │────│ Secure Unix Peer Socket  │
                                                   └───┬──────────────────────┘    └─────────────┬────────────┘
                                                       │                                         │
                                                       ▼                                         ▼
                                           ┌───────────────┐                       ┌──────────────────────────┐
                                           │  Git Rollback │                       │    MCP Core Gateway      │
                                           │  State Engine │                       │  (SO_PEERCRED Governed)  │
                                           └───────────────┘                       └──────────────────────────┘
```

---

## Core Pillars & Architectural Mapping

### 1. Process Virtualization & Lifecycle Management
High-autonomy agents execute in short, bursts of highly parallel and volatile processes. We delegate lifecycle management completely to **systemd user slices** and **cgroups v2** profiles.
*   **Transient Unit Spawning:** Agents run inside dynamically generated transient scopes (`systemd-run --user`) ensuring CPU, Memory, and IO footprint limits map to real operating system resources.
*   **Unified Audits:** Every process output stream (stdout/stderr) automatically funnels into `systemd-journald` for cryptographically signed, immutable logging.

### 2. Resource Sandboxing & Secure Execution
To prevent malicious code execution or context leaking, workspace directories run inside ephemeral containerized boundaries.
*   **Rootless Podman Containment:** Safe execution using standard OCI runtime configurations without requiring superuser privilege.
*   **SELinux Profiles via Udica:** Custom-tailored multi-category security domains (MCS) dynamically constructed for each agent's execution parameters, restricting lateral movement on the host filesystem.

### 3. Desktop Authorization & User Protection
Before an AI makes an elevated modification, system control must verify approval without interrupting developer speed.
*   **Polkit (PolicyKit) Integration:** Desktop GUI dialogs and terminal password prompts are triggered as standard system authorization steps before letting agents run untrusted API or shell hooks.
*   **Multi-Tier Trust Models:** Execution domains split into unified target tiers:
    *   `TRUST_0` (System Admin / No Containment)
    *   `TRUST_1` (Developer Desktop Workspaces)
    *   `TRUST_2` (Supervised Sandboxes with User Confirmation)
    *   `TRUST_3` (Strict Read-Only Sandboxes)
    *   `TRUST_4` (Completely Air-Gapped / Synthetic Mocks)

### 4. Transactional Workspace Recovery
We replace expensive backup solutions with git-as-a-state-engine.
*   **Atomic Rollback Trees:** BuildAIOS wraps active code directories inside lightweight, local Git engines tracked by our State Reconciler daemon. 
*   **Zero-Overhead Reversions:** Programmatic resets (`git reset --hard`) restore complex directory states across hundred-file codebases in sub-millisecond durations when tests fail or an agent drifts.

### 5. Multi-Inference Coexistence
BuildAIOS acts as a direct proxy routing optimization.
*   **Coexistence Daemons:** Unified abstraction wrappers over local `vLLM` server arrays and background `Ollama` services. Agents query a single endpoint that manages runtime allocation dynamically based on target GPU constraints.

---

## The Primary Differentiator: MCP Gateway Core Proxy

The core engine of BuildAIOS is the **UNIX Domain Socket Model Context Protocol (MCP) Core Proxy**. Unlike simple network relays, the gateway executes high-integrity validation directly inside the OS network socket layer:

*   **SO_PEERCRED Verification:** Uses kernel socket checks (`socket.SO_PEERCRED`) to immediately identify the executing process PID, UID, and GID on every tool invocation. It enforces security policies based on exactly *which* systemd scope or Podman namespace is sending the request.
*   **Dynamic Token Injection:** Prevents sensitive API keys (OpenAI, Anthropic, GitHub) from leaking onto file systems. Sockets capture process tokens at runtime from secure memory maps via the host's **GNOME Keyring (libsecret)** daemon, binding credentials only for the lifespan of that specific socket transaction.
*   **Synchronous Schema Enforcement:** Prevents raw tool execution loops from presenting corrupt parameters to host system calls. Handlers parse, validate, and check execution structures against strictly controlled JSON blueprints before tools fire.

---

## Repository Architecture

```text
~/fedora-ai-os/
├── project_state/                # Authoritative Ground Truth (Governance & Blueprints)
│   ├── CURRENT_STATE.md          # Active lifecycle development phase tracking
│   ├── CRITICAL_PATH.md          # Core architecture rules & item exclusions
│   ├── NEXT_ACTIONS.md           # Tactical backlog of development actions
│   └── ARCHITECTURE_INDEX.md     # Indexes all components mapping control/data planes
│
├── implementation_code/          # High-grade component implementations
│   ├── phase0/                   # Completed: State reconcilers, suspension engines, chaos hooks
│   └── phase1/                   # Active: Async UNIX Socket MCP Gateway, schema validators, Polkit wrappers
│
└── roles/                        # Technical domain divisions
    └── DEPARTMENT_BRIEFS.md      # Team assignments (QA, Security, DevEx, Systems Core)
```

---

## Quickstart: Building & Serving Phase 1

Deploy the Core Proxy and security boundaries locally:

### Prerequisites
*   Fedora Linux (Workstation or Silverblue)
*   Python 3.11+
*   Systemd & Podman

### Setup & Run
1.  Navigate into the gateway development workspace:
    ```bash
    cd ~/fedora-ai-os/implementation_code/phase1/mcp-gateway
    ```
2.  Install the package in editable mode:
    ```bash
    pip install -e .
    ```
3.  Bootstrap the async UNIX socket listener:
    ```bash
    gateway serve
    ```
    *   This mounts the fast socket gateway at `/var/run/buildaios/mcp-gateway.sock` (or user runtime path) and serves an internal health and status verification endpoint on port `8000`.

---

## Operational Roadmap & Milestones

| System Component | Scope Boundary | Host Mechanism | Status |
| :--- | :--- | :--- | :--- |
| **State Reconciler** | Transactional workspace Rollbacks | Git & Btrfs snapshot hooks | **Complete** |
| **MCP Socket Gateway** | Secure JSON-RPC Tool Routing | Kernel `SO_PEERCRED` checks | **In Progress** |
| **Memory Layer** | 4-Tier Cognition + Docs2DB DB | RAG over local Vector Engine | **Planned** |
| **Containment Box** | Dynamic Agent Sandbox | Rootless Podman + Udica SELinux | **Planned** |
| **Security Layer** | Multi-Tier Trust Models | Polkit + GOM / libsecret | **Planned** |

---

## Core Engineering Division

*   **Lead Architect / Integrator:** Lakshay Dabas
*   **Systems Integrity & MCP Gateway Dev:** Lakshay Bharti
*   **Security & SELinux Confinement:** Ojasvi
*   **QA & Automated Resilience Testing:** Jatin
*   **Developer Experience (DevEx) & Tooling:** Kapil
