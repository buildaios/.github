# Contributing to BuildAIOS

Welcome! We are thrilled that you are interested in contributing to BuildAIOS.

BuildAIOS is an open-source, governed AI agent runtime and cognitive control plane built above Fedora Linux. By contributing, you help us design and implement a secure, recoverable, and transparent platform for governed AI agent execution.

### Table of Contents
1. [Ways to Contribute](#ways-to-contribute)
2. [Repository Structure](#repository-structure)
3. [Development Workflow](#development-workflow)
4. [Branch Naming Convention](#branch-naming-convention)
5. [Commit Message Guidelines](#commit-message-guidelines)
6. [Pull Request Process](#pull-request-process)
7. [Documentation Standards](#documentation-standards)
8. [Code Quality & Testing Expectations](#code-quality--testing-expectations)
9. [Communication & Issue Reporting](#communication--issue-reporting)
10. [Review Process & Community Values](#review-process--community-values)

---

## Ways to Contribute

We welcome diverse contributions across several dimensions:
* **Code:** Fixing bugs, writing features, or implementing core engine capabilities.
* **Testing:** Writing pytest suites, integration testing Podman profiles, or trying out new chaos engineering scripts.
* **Environment Packs:** Defining unprivileged OCI container structures and SELinux templates (udica) for specialized agent environments.
* **Documentation:** Refining our architecture specifications, developer runbooks, or security configurations.
* **Triage:** Helping reproduce issues, clarifying user bug reports, and managing labels.

---

## Repository Structure

Our organization hosts separated, highly focused workspaces. Keep implementations aligned to their target scope:

* **`.github`**: Global community documents, issue templates, and centralized CI/CD workflows.
* **`runtime-agent`**: The transaction-safe atomic execution engine (`v2_engine.py`, `v3_engine.py`), workflow orchestrators, and backup-and-restore systems.
* **`mcp-gateway`**: Core JSON-RPC routing gateway over UNIX domain sockets with kernel peer credentials checks and schema validations.
* **`docs`**: Source documents for system architecture blueprints, decisions (`references/architecture_decisions.md`), and API standards.
* **`aios-website`**: The Next.js 16/React-based marketing landing page, featuring Tailwind CSS and Framer Motion components.

---

## Development Workflow

1. **Setup Workspace:** Verify your system has Node 22+ and Python 3.14+ installed. Ensure Podman is set up in rootless mode on your Fedora system.
2. **Find an Issue:** Look for issues tagged `good-first-issue` or items in our active `CRITICAL_PATH.md`.
3. **Fork & Clone:** Clone your fork locally and set the upstream remote:
   ```bash
   git remote add upstream https://github.com/buildaios/buildaios.git
   ```
4. **Synchronize:** Keep your local branch up to date with `main`:
   ```bash
   git fetch upstream
   git checkout main
   git merge upstream/main
   ```
5. **Create Branch:** Create a local working branch based on `main` using our tracking conventions.

---

## Branch Naming Convention

Keep your branches linked to active tracking items. Use the format:
`<type>/<issue-number>-<short-description>`

**Allowed Types:**
* `feat/` — Adding new features or systems (e.g., `feat/102-mcp-unix-socket`).
* `fix/` — Bugs, memory leaks, systemd failures (e.g., `fix/88-flock-zombie-deadlock`).
* `test/` — Writing pytest cases, stress runs (e.g., `test/91-chaos-monkey`).
* `docs/` — Editing specifications or markdown references (e.g., `docs/12-udica-selinux-guide`).

---

## Commit Message Guidelines

We enforce the Conventional Commits specification (v1.0.0). This generates clean automated changelogs.

**Format:**
```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

**Allowed Types:**
* `feat`: A new user-facing capability (e.g., `feat(mcp): implement kernel SO_PEERCRED lookup`).
* `fix`: A bug fix or reconciliation adjustment.
* `test`: Adding or correcting tests with zero functional code changes.
* `docs`: Documentation-only updates.
* `refactor`: Structural changes that neither fix bugs nor add new features.
* `chore`: Updating dependencies, packaging files, or build parameters.

**Scope Examples:** `engine`, `mcp`, `security`, `selinux`, `docs`, `website`.

*Tip: A well-written commit message is descriptive and uses the imperative mood: "fix(engine): close file descriptor on abort" rather than "fixed engine file descriptor."*

---

## Pull Request Process

1. **Incremental Changes:** Choose surgical adjustments over major refactors.
2. **Link Issues:** Always link your PR to an active GitHub issue in the footer (e.g., `Closes #102`).
3. **Run Self-Checks:** Ensure lint rules, code formatter, and pytest run locally without failure before pushing.
4. **Draft Phase:** Open as a Draft PR if seeking early review or testing feedback. Mark as "Ready for Review" once complete.
5. **No Force Pushes post-Review:** Once comments have been left, append additional corrections as separate commits. Avoid force-pushing when possible to keep review histories readable.

---

## Documentation Standards

* **Keep It Programmatic:** Always pair ParagraphStyle fontSize adjustments with proportional leading increases (`leading = fontSize * 1.25`) to avoid text collisions.
* **No Markdown for Out-Of-Band Platforms:** When writing for channels that render raw text (like notification bridges), favor bolding and lists over markdown headings and table grids.
* **Maintain the Source of Truth:** Up-to-date states reside in `/Docs/project-state/`. If implementing changes that impact our project stages, proactively file updates to `HEARTBEAT.md` or `CURRENT_STATE.md`.

---

## Code Quality & Testing Expectations

Every functional contribution must prove its safety under stress. We do not ship code without testing.
* **Atomic Safeguards:** Ensure all configuration-state operations leverage safe temporary writes, fsync guards, and auto-fallback backups (`.bak`).
* **Pytest Coverage:** New features require matching pytest coverage. Ensure custom actions implement a valid deterministic `compensate()` routine for rollback safety during execution engine faults.
* **Non-Blocking Checks:** Never block on input windows or prompt dialogs. Write pure non-interactive CLI sequences that can be evaluated entirely within continuous integration pipelines.

---

## Communication & Issue Reporting

* **Live Discussions:** Share ideas, propose architectural improvements, or show off concepts under our GitHub Discussions channels.
* **Urgent Vulnerabilities:** Do not open public issues for security vulnerabilities. Send detailed reports privately to: **security@buildaios.dev**.
* **Bug Claims:** When filing bug reports, include step-by-step reproduction blocks including precise host kernels, Python, and Podman versions.

---

## Review Process & Community Values

* **Asymmetric Architecture:** We favor mass, thick, and highly visible structure over unnecessary network synchronization protocols.
* **Build over Audit:** Real software execution takes priority over lengthy audit checklists. We review your pull requests by inspecting execution output, verified performance metrics, and testing compliance.
* **Direct Feedback:** We value transparent, minimal, and technical communication. Let the working code and clean tests speak for themselves.
