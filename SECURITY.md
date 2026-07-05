# Security Policy — BuildAIOS

As a governed AI agent runtime and cognitive control plane operating on Fedora Linux, security is a core pillar of BuildAIOS. We take vulnerabilities and system escapes extremely seriously. We are committed to a transparent, structured, and responsible disclosure process to keep our runtime and host systems secure.

---

## Supported Versions

We actively maintain and support the following core components of the BuildAIOS system:

| Component | Supported Version | Status |
|---|---|---|
| **runtime-agent** | >= 0.2.0 | Maintained (Active Phase 0/1) |
| **mcp-gateway** | >= 0.1.0 | Maintained (Active Phase 1) |
| **aios-website** | >= 1.0.0 | Maintained |

Older pre-releases and proof-of-concept repositories outside this scope are considered legacy and should not be run in production environments.

---

## Reporting Vulnerabilities

If you discover a security vulnerability or system escape inside BuildAIOS, **do NOT open a public GitHub issue**. Doing so risks exposing systems before a security patch can be validated and deployed.

Instead, please report your findings privately.

### Private Disclosure Process
1. Draft an email outlining the vulnerability details.
2. Send the report to: **security@buildaios.dev**
3. Include the following critical diagnostics for fast processing:
   * A detailed description of the vulnerability, escape vector, or privilege escalation.
   * Step-by-step reproduction instructions (ideally inside a clean rootless Podman environment).
   * Host kernel, systemd, and Python configurations.
   * The potential impact on host configurations or the MCP Socket Gateway.

---

## Response Timeline

We commit to a swift response cycle:
* **Initial Acknowledgement:** Within 48 hours of your submission, we will acknowledge receipt and verify we can reproduce the state.
* **Triage & Evaluation:** Within 5 business days, we will provide a preliminary severity evaluation (using CVSS v3.1 standards) and an estimate of the remediation timeline.
* **Patch Deployment:** We aim to release validated security patches for critical vulnerabilities within 30 days of discovery.
* **Public Advisory:** A security advisory will be published once the patch has been tested, deployed, and coordinate disclosures are finalized.

---

## What NOT to Report

The following behaviors or out-of-scope issues should not be reported via active security channels:
* Malformed JSON-RPC requests that result in standard validation exceptions or circuit-breaker halts on the MCP Gateway (these are intended safeguards, not vulnerabilities).
* Standard SELinux denials in permissive mode (udica templates must be evaluated in targeted domains).
* Issues regarding third-party models, providers, or custom API endpoints outside the core BuildAIOS repository.

---

## Responsible Disclosure

We ask that you follow responsible disclosure guidelines:
* Give us reasonable time (as outlined in our timeline) to resolve the issue before making any details public.
* Avoid accessing, modifying, or destroying user data during validation steps.
* Do not conduct denial of service (DoS) attempts or target public-facing landing zones.

---

## Security Acknowledgements

We appreciate the rigorous work of security researchers and open-source contributors. Unless requested otherwise, all researchers who find and report verified vulnerabilities under our security policy will be credited and publicly thanked in our security advisories and release logs.
