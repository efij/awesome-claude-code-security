<div align="center">

# Awesome Claude Code Security

[![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re)
[![Track Awesome List](https://www.trackawesomelist.com/badge.svg)](https://www.trackawesomelist.com/awesome-claude-code-security)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Last Commit](https://img.shields.io/github/last-commit/anthropics/claude-code.svg?label=upstream%20activity)](https://github.com/anthropics/claude-code)

**A curated collection of security resources, hardening tools, threat research, and governance frameworks for [Claude Code](https://code.claude.com) and the AI coding agent ecosystem.**

*For security engineers, AppSec teams, platform engineers, and anyone deploying Claude Code in production.*

[Official Docs](#-official-security-documentation) · [Hardening](#-hardening-and-permissions) · [MCP Security](#-mcp-security) · [Tools](#-security-tools-and-scanners) · [Enterprise](#-enterprise-governance-and-policy) · [Research](#-research-talks-and-writeups)

</div>

---

> **Why this list?** Claude Code runs shell commands, edits files, calls APIs, and installs MCP servers — all with your user privileges. One malicious `.claude/settings.json`, a poisoned MCP tool, or a prompt injection hidden in a README can lead to RCE, credential theft, or silent data exfiltration. This list exists to help you harden, govern, and monitor every surface.

---

## Contents

- [📋 Official Security Documentation](#-official-security-documentation)
- [🔒 Hardening and Permissions](#-hardening-and-permissions)
- [📦 Sandboxing and Isolation](#-sandboxing-and-isolation)
- [🪝 Hooks and Guardrails](#-hooks-and-guardrails)
- [🔌 MCP Security](#-mcp-security)
- [💉 Prompt Injection and Agent Threats](#-prompt-injection-and-agent-threats)
- [🔑 Secrets and Data Leakage](#-secrets-and-data-leakage)
- [🏢 Enterprise Governance and Policy](#-enterprise-governance-and-policy)
- [⚙️ Secure CI/CD and Automation](#️-secure-cicd-and-automation)
- [📦 Plugins, Extensions, and Supply Chain](#-plugins-extensions-and-supply-chain)
- [🤖 Agent Orchestration and Loop Safety](#-agent-orchestration-and-loop-safety)
- [🖥️ OS and Endpoint Hardening](#️-os-and-endpoint-hardening)
- [🛠️ Security Tools and Scanners](#️-security-tools-and-scanners)
- [🐛 Vulnerability Research and Disclosures](#-vulnerability-research-and-disclosures)
- [📐 Frameworks and Standards](#-frameworks-and-standards)
- [📚 Research, Talks, and Writeups](#-research-talks-and-writeups)
- [🔄 Competitor and Adjacent Controls](#-competitor-and-adjacent-controls)
- [✅ Checklists and Templates](#-checklists-and-templates)
- [🌐 Community and Ecosystem](#-community-and-ecosystem)

---

## 📋 Official Security Documentation

*Core security documentation published by Anthropic.*

- [Security Overview](https://code.claude.com/docs/en/security) - Architecture reference covering permission model, sandboxing, prompt injection defenses, and privacy safeguards.
- [Configure Permissions](https://code.claude.com/docs/en/permissions) - Tiered Allow/Ask/Deny system with tool-specific rules, wildcard patterns, and precedence evaluation.
- [Sandboxing](https://code.claude.com/docs/en/sandboxing) - Filesystem and network isolation using Linux bubblewrap and macOS Seatbelt with domain restrictions.
- [Hooks Reference](https://code.claude.com/docs/en/hooks) - PreToolUse, PostToolUse, and ConfigChange hook events for security automation.
- [Hooks Guide](https://code.claude.com/docs/en/hooks-guide) - Practical patterns: permission enforcement, injection detection, audit logging.
- [Settings](https://code.claude.com/docs/en/settings) - Hierarchical config scopes (Managed > CLI > Local > Project > User) and sensitive file protection.
- [Authentication](https://code.claude.com/docs/en/authentication) - Credential management, secure storage, apiKeyHelper, and enterprise SSO.
- [Data Usage](https://code.claude.com/docs/en/data-usage) - Retention policies, TLS + AES-256 encryption, telemetry, and training opt-out.
- [Zero Data Retention](https://code.claude.com/docs/en/zero-data-retention) - Enterprise immediate data deletion with HIPAA BAA coverage.
- [Monitoring and Usage](https://code.claude.com/docs/en/monitoring-usage) - OpenTelemetry integration for session tracking, token usage, and audit trails.
- [MCP Configuration](https://code.claude.com/docs/en/mcp) - MCP server setup, OAuth 2.0, scope hierarchy, enterprise allowlists/denylists.
- [Claude Code on the Web](https://code.claude.com/docs/en/claude-code-on-the-web) - Cloud execution: isolated VMs, network proxies, git push restrictions, domain allowlists.
- [Amazon Bedrock Integration](https://code.claude.com/docs/en/amazon-bedrock) - IAM policies, AWS Guardrails, credential management, model version pinning.

### Anthropic Engineering & Blog

- [Claude Code Security Features](https://www.anthropic.com/news/claude-code-security) - Vulnerability detection: codebase scanning, multi-stage verification; found 500+ vulnerabilities in production code.
- [Making Claude Code Secure and Autonomous](https://www.anthropic.com/engineering/claude-code-sandboxing) - Engineering deep dive on filesystem isolation, network proxy, OS-level enforcement, credential exfiltration defense.
- [Automate Security Reviews with Claude Code](https://www.anthropic.com/news/automate-security-reviews-with-claude-code) - Using Claude Code Security as an automated reviewer in CI pipelines.

## 🔒 Hardening and Permissions

*Configs, frameworks, and guides for locking down Claude Code.*

- [Trail of Bits claude-code-config](https://github.com/trailofbits/claude-code-config) - Opinionated production defaults from a top security firm: sandboxing, permissions, hooks, skills, MCP server configs. The gold standard for secure setups.
- [Claude Code Organizer](https://github.com/mcpware/claude-code-organizer) - Visual scope audit for ~/.claude/ configs. Detects cross-scope contamination where memories, skills, or MCP entries leak between projects, reducing unintended context exposure and stale permission inheritance.
- [claude-code-security](https://github.com/marc-shade/claude-code-security) - Progressive hardening framework covering agent config protection, hooks, runtime security, injection prevention, and supply chain controls.
- [everything-claude-code](https://github.com/affaan-m/everything-claude-code) - Performance optimization system with security components: skills, instincts, memory, and research-first development patterns.
- [Claude Code Ultimate Guide](https://github.com/FlorianBruniaux/claude-code-ultimate-guide) - Comprehensive documentation with production-ready templates including security hardening configs.
- [Hardening Claude Code: Security Review Framework](https://medium.com/@emergentcap/hardening-claude-code-a-security-review-framework-and-the-prompt-that-does-it-for-you-c546831f2cec) - Security review methodology with a ready-to-use audit prompt.
- [StepSecurity: Securing Claude Code in GitHub Actions](https://www.stepsecurity.io/blog/anthropics-claude-code-action-security-how-to-secure-claude-code-in-github-actions-with-harden-runner) - Harden-Runner integration for network monitoring and tamper-proof logs in CI.
- [Cycode: Anthropic Claude Code Security & AppSec](https://cycode.com/blog/anthropic-claude-code-security-appsec/) - Analysis of Claude Code's security model from an AppSec vendor perspective.
- [Snyk: Why Claude Code Security Is Great News](https://snyk.io/articles/anthropic-launches-claude-code-security/) - Industry analysis of Anthropic's security capabilities and what they mean for secure development.

## 📦 Sandboxing and Isolation

*Isolating AI agent code execution from your host system.*

- [Arrakis](https://github.com/abshkbh/arrakis) - Self-hosted MicroVM sandbox for AI agents with backtracking, REST API, Python SDK, and Firecracker-based isolation.
- [microsandbox](https://github.com/zerocore-ai/microsandbox) - Open-source self-hosted MicroVM sandboxes with sub-200ms startup, hardware-level isolation via libkrun. ~3.3k stars.
- [agent-infra/sandbox](https://github.com/agent-infra/sandbox) - All-in-one Docker sandbox for AI agents: browser, shell, file, MCP, and VS Code server in a container.
- [sandbox-agent (Rivet)](https://github.com/rivet-dev/sandbox-agent) - Run Claude Code and other coding agents in sandboxes controlled over HTTP.
- [codeduet-microvm-ai-agent-sandbox](https://github.com/CodeDuet/codeduet-microvm-ai-agent-sandbox) - MicroVM sandbox using Cloud Hypervisor with Linux and Windows guest support and hardware-level isolation.
- [Kubernetes agent-sandbox](https://github.com/kubernetes-sigs/agent-sandbox) - Kubernetes CRD for declarative sandbox management with persistent identity for AI agents.
- [SWE-ReX](https://github.com/SWE-agent/SWE-ReX) - Sandboxed shell environments for AI code agents with parallel execution and cloud deployment support.
- [awesome-sandbox](https://github.com/restyler/awesome-sandbox) - Curated list of code sandboxing solutions for AI, comparing isolation approaches.
- [How to Sandbox AI Agents in 2026](https://northflank.com/blog/how-to-sandbox-ai-agents) - Technical comparison: MicroVMs vs gVisor vs hardened containers for agent isolation.
- [Best Code Execution Sandbox for AI Agents](https://northflank.com/blog/best-code-execution-sandbox-for-ai-agents) - Ranked comparison of sandbox platforms with security/performance tradeoffs.

## 🪝 Hooks and Guardrails

*Hook systems and runtime enforcement for Claude Code.*

- [claude-code-safety-net](https://github.com/kenryu42/claude-code-safety-net) - Plugin intercepting destructive git/filesystem commands before execution. Semantic argument parsing distinguishes safe from dangerous operations.
- [Lasso claude-hooks](https://github.com/lasso-security/claude-hooks) - Prompt injection defense hooks: scans files, web fetches, and command output in real-time. Detects 50+ injection patterns in READMEs, HTML comments, and docs.
- [claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) - Advanced hook patterns and techniques for Claude Code security automation.
- [claudekit](https://github.com/carlrannaberg/claudekit) - Toolkit of custom commands, hooks, and security utilities for Claude Code.
- [claude-code-hooks-multi-agent-observability](https://github.com/disler/claude-code-hooks-multi-agent-observability) - Real-time monitoring for multi-agent Claude Code sessions via hook event tracking.
- [claude-code-showcase](https://github.com/ChrisWiles/claude-code-showcase) - Comprehensive project configuration example with hooks, skills, agents, commands, and GitHub Actions workflows.
- [NeMo Guardrails](https://github.com/NVIDIA-NeMo/Guardrails) - NVIDIA's toolkit for programmable LLM guardrails with Colang language for dialog flow control. ~4.5k stars.

## 🔌 MCP Security

*Securing the Model Context Protocol ecosystem.*

### Scanners and Auditors

- [Snyk agent-scan](https://github.com/snyk/agent-scan) - Professional security scanner for AI agents, MCP servers, and skills covering 15+ risk categories.
- [mcp-scan (Invariant Labs)](https://github.com/invariantlabs-ai/mcp-scan) - MCP security scanner with proxy mode for real-time scanning without infrastructure changes.
- [Cisco MCP Scanner](https://github.com/cisco-ai-defense/mcp-scanner) - Cisco's scanner for detecting threats and security findings in MCP servers.
- [MCP Security Scanner (SARIF)](https://github.com/nostalgicskinco/mcp-security-scanner) - Static + dynamic checks for path traversal, auth gaps, prompt injection. Outputs SARIF for GitHub code scanning.
- [AWS MCP Security Scanner](https://github.com/aws-samples/sample-mcp-security-scanner) - Integrates Checkov, Semgrep, and Bandit for comprehensive code security analysis via MCP.
- [SecureMCP](https://github.com/makalin/SecureMCP) - Audit MCP for OAuth leaks, prompt injection, rogue servers, and tool poisoning.
- [mcpserver-audit](https://github.com/ModelContextProtocol-Security/mcpserver-audit) - Pre-use safety examination tool with vulnerability database.
- [MCP Security Audit (npm)](https://github.com/qianniuspace/mcp-security-audit) - Audits npm dependencies in MCP servers for known vulnerabilities via registry.

### Gateways and Proxies

- [Microsoft MCP Gateway](https://github.com/microsoft/mcp-gateway) - Reverse proxy for MCP servers in Kubernetes with OAuth 2.0 (Azure Entra ID), RBAC, and session-aware routing.
- [Hypr MCP Gateway](https://github.com/hyprmcp/mcp-gateway) - OAuth proxy with dynamic client registration, prompt analytics, and MCP firewall for enterprise-grade servers.
- [Secure MCP Gateway (Enkrypt)](https://github.com/enkryptai/secure-mcp-gateway) - Admin-level gateway with guardrails at each MCP server to block injection, exfiltration, and unauthorized access.
- [Lasso MCP Gateway](https://github.com/lasso-security/mcp-gateway) - Plugin-based gateway that intercepts and sanitizes sensitive information across MCP orchestration.
- [IBM ContextForge](https://ibm.github.io/mcp-context-forge/) - Open-source registry and proxy federating MCP/A2A/REST APIs with centralized governance and discovery.
- [awesome-mcp-gateways](https://github.com/e2b-dev/awesome-mcp-gateways) - Curated list of MCP gateway products and solutions.

### Standards and Checklists

- [MCP Server Security Standard (MSSS)](https://github.com/mcp-security-standard/mcp-server-security-standard) - Open, testable certification standard with compliance levels and evidence requirements.
- [MCP Security Checklist (SlowMist)](https://github.com/slowmist/MCP-Security-Checklist) - Comprehensive checklist: input validation, rate limiting, RBAC, credential management, container hardening.
- [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security) - Curated collection of MCP vulnerabilities, articles, tools, and best practices. ~660 stars.
- [spring-ai MCP Security](https://github.com/spring-ai-community/mcp-security) - Authorization framework for MCP client/server using Spring Security.

### Research

- [Pillar Security: MCP Security Risks](https://www.pillar.security/blog/the-security-risks-of-model-context-protocol-mcp) - Threat analysis: tool poisoning, rug pulls, credential theft, cross-server manipulation.
- [Invariant Labs: Tool Poisoning Attacks](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks) - Agent hijacking via malicious tool descriptions, WhatsApp exploit, "Rug Pull" mutation attacks.
- [Simon Willison: MCP Prompt Injection](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/) - Practical analysis of confused deputy attacks in MCP tool integrations.
- [Invariant Labs: GitHub MCP Vulnerability](https://invariantlabs.ai/blog/mcp-github-vulnerability) - Exploiting MCP to access private GitHub repositories.
- [Netskope: Invisible Backdoors in MCP](https://www.netskope.com/blog/securing-llm-superpowers-the-invisible-backdoors-in-mcp) - Hidden backdoor mechanisms in MCP server implementations.
- [Systematic Analysis of MCP Security (arXiv)](https://arxiv.org/html/2508.12538v1) - Academic systematic analysis of MCP security threats and defenses.
- [MCPTox: Benchmark for Tool Poisoning (arXiv)](https://arxiv.org/html/2508.14925v1) - Academic benchmark for evaluating tool poisoning attacks on real-world MCP servers.

## 💉 Prompt Injection and Agent Threats

*Attacks and defenses for AI coding agents.*

### Claude Code Specific

- [Caught in the Hook: RCE via Claude Code Project Files](https://research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files-cve-2025-59536/) - Check Point: three critical CVEs — RCE via MCP config, RCE via hooks, and API key harvesting.
- [Lasso claude-hooks](https://github.com/lasso-security/claude-hooks) - Real-time prompt injection detection for Claude Code: 50+ patterns across files, web fetches, and docs.

### Tools and Frameworks

- [promptfoo](https://github.com/promptfoo/promptfoo) - CLI for red-teaming LLM apps. Adaptive attack generation, CI/CD integration. Used by Shopify, Discord, Microsoft. ~6k stars.
- [Garak](https://github.com/NVIDIA/garak) - NVIDIA-backed red-teaming toolkit: 37+ probe modules for injection, jailbreaks, encoding bypasses, data extraction. Apache 2.0.
- [PyRIT (Microsoft)](https://github.com/Azure/PyRIT) - Python Risk Identification Tool for generative AI. Enterprise red-teaming framework for Azure environments.
- [Rebuff (Protect AI)](https://github.com/protectai/rebuff) - Multi-layered prompt injection detection: heuristics, LLM analysis, vector DB of known attacks, canary tokens.
- [HouYi](https://github.com/LLMSecurity/HouYi) - Automated prompt injection testing framework for LLM-integrated applications.
- [Open-Prompt-Injection](https://github.com/liu00222/Open-Prompt-Injection) - Academic benchmark with DataSentinel and PromptLocate defenses.
- [promptmap](https://github.com/utkusen/promptmap) - Security scanner for custom LLM apps. White-box and black-box prompt injection testing.
- [awesome-prompt-injection](https://github.com/Joe-B-Security/awesome-prompt-injection) - Curated resource on prompt injection vulnerabilities in ML models.
- [tldrsec/prompt-injection-defenses](https://github.com/tldrsec/prompt-injection-defenses) - Every practical and proposed defense against prompt injection, maintained by tl;dr sec.

### Research

- [OWASP LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) - Canonical definition and threat model. The #1 risk in 73% of production AI deployments.
- [DEF CON 33 / Black Hat 2025: AgentFlayer](https://www.csoonline.com/article/4037869/5-key-takeaways-from-black-hat-usa-2025.html) - Zenity research: 0-click attacks on enterprise AI assistants including Copilot and Gemini.

## 🔑 Secrets and Data Leakage

*Preventing credential exposure, data exfiltration, and transcript leakage.*

### Prevention Tools

- [TruffleHog](https://github.com/trufflesecurity/trufflehog) - Find, verify, and analyze leaked credentials. 800+ secret types, live verification. Essential for pre-commit scanning in AI workflows. ~18k stars.
- [Gitleaks](https://github.com/gitleaks/gitleaks) - Fast secrets scanner using regex and entropy. High precision, low false positives. ~19k stars.
- [ggshield (GitGuardian)](https://github.com/GitGuardian/ggshield) - Detect 500+ secret types with advanced validation. Pre-commit hooks, CI integration, and real-time scanning.
- [LLM Guard (Protect AI)](https://github.com/protectai/llm-guard) - Input/output security toolkit: PII detection, toxicity filtering, secrets scanning for LLM interactions. ~4k stars.
- [ml-model-data-leak-layer](https://github.com/AashiqRamachandran/ml-model-data-leak-layer) - PII leak detection in LLM-generated content using ML and regex patterns.
- [GitHub Secret Protection](https://github.blog/changelog/2025-03-04-introducing-github-secret-protection-and-github-code-security/) - Push protection with AI-powered detection. Enabled by default on public repos since 2024.

### Claude Code Specific

- [Data Usage and Privacy](https://code.claude.com/docs/en/data-usage) - Official data flows: retention policies, encryption, telemetry controls, training opt-out.
- [Zero Data Retention](https://code.claude.com/docs/en/zero-data-retention) - Enterprise immediate data deletion post-session with HIPAA BAA.
- [Sensitive File Protection](https://code.claude.com/docs/en/settings) - Configure deny patterns for `.env`, credentials, SSH keys to prevent Claude Code access.
- [CVE-2026-21852: API Key Harvesting](https://research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files-cve-2025-59536/) - Demonstrated API key extraction from Claude Code sessions via crafted project files.

## 🏢 Enterprise Governance and Policy

*Rolling out Claude Code securely across teams and organizations.*

- [Managed Settings](https://code.claude.com/docs/en/settings) - Enterprise-enforced config: managed policies override all scopes, controlling permissions, sandboxing, MCP.
- [Monitoring and Audit](https://code.claude.com/docs/en/monitoring-usage) - OpenTelemetry audit trails: session tracking, token usage, cost metrics, multi-team support.
- [Authentication and SSO](https://code.claude.com/docs/en/authentication) - SAML 2.0, OIDC, enterprise credential management, identity provider integration.
- [Microsoft Agent Governance Toolkit](https://github.com/microsoft/agent-governance-toolkit) - Zero-trust policy enforcement, identity management, execution sandboxing. Covers OWASP Agentic Top 10.
- [GitHub Enterprise AI Controls](https://github.blog/changelog/2026-02-26-enterprise-ai-controls-agent-control-plane-now-generally-available/) - GA agent control plane: MCP allowlists, audit logs, RBAC, session monitoring for Copilot.
- [GitHub AI Governance Framework](https://resources.github.com/learn/pathways/copilot/essentials/empower-developers-with-ai-policy-and-governance/) - Creating organizational AI policy and governance for coding assistants.
- [IBM + Anthropic Enterprise Partnership](https://newsroom.ibm.com/2025-10-07-2025-ibm-and-anthropic-partner-to-advance-enterprise-software-development-with-proven-security-and-governance) - Enterprise governance integration with IBM security and compliance capabilities.
- [NVIDIA Safety for Agentic AI](https://github.com/NVIDIA-AI-Blueprints/safety-for-agentic-ai) - Blueprint for improving safety, security, and privacy at build, deploy, and run stages.
- [Claude Enterprise Deployment Guide](https://www.datastudios.org/post/claude-enterprise-security-configurations-and-deployment-controls-explained) - Enterprise security configurations and deployment controls explained.

## ⚙️ Secure CI/CD and Automation

*Running Claude Code safely in pipelines and automated workflows.*

- [claude-code-action](https://github.com/anthropics/claude-code-action) - Official GitHub Action for CI/CD. v1.0: auto mode detection, interactive + automation modes.
- [claude-code-security-review](https://github.com/anthropics/claude-code-security-review) - Official AI-powered security review Action for PRs. OWASP-aligned analysis, found vulnerabilities in Claude Code itself.
- [GitHub Actions Docs](https://code.claude.com/docs/en/github-actions) - Official reference for Claude Code in GitHub Actions: triggers, configuration, permissions.
- [StepSecurity Harden-Runner](https://www.stepsecurity.io/blog/anthropics-claude-code-action-security-how-to-secure-claude-code-in-github-actions-with-harden-runner) - Network monitoring and tamper-proof audit logs for Claude Code Actions — critical since claude-code-action has unrestricted network access.
- [CLAUDE.md CI/CD Wiki](https://github.com/ruvnet/ruflo/wiki/CLAUDE-MD-CICD) - Community patterns for CLAUDE.md configuration in CI/CD pipelines.
- [Claude Code Headless Mode](https://code.claude.com/docs/en/cli-usage) - Non-interactive `--print` and `-p` flags for scripted security workflows and automation.

## 📦 Plugins, Extensions, and Supply Chain

*Managing trust and risk in the Claude Code plugin ecosystem.*

- [Plugin Discovery & Trust Model](https://code.claude.com/docs/en/discover-plugins) - Official plugin marketplace: trust considerations, managed restrictions, organizational controls.
- [claude-plugins-official](https://github.com/anthropics/claude-plugins-official) - Anthropic's official managed plugin directory.
- [claude-code-safety-net](https://github.com/kenryu42/claude-code-safety-net) - Supply-chain safety plugin: intercepts destructive commands before execution.
- [MCP Server Security Standard](https://github.com/mcp-security-standard/mcp-server-security-standard) - Certification framework for MCP servers with compliance levels and evidence schemas.
- [awesome-claude-code-plugins](https://github.com/ccplugins/awesome-claude-code-plugins) - Curated list of slash commands, subagents, MCP servers, and hooks.
- [Trail of Bits Skills](https://github.com/trailofbits/skills) - Security research skills for Claude Code: vulnerability detection and audit workflows from Trail of Bits.
- [Sonatype Guide MCP](https://code.claude.com/docs/en/discover-plugins) - Software supply chain intelligence: dependency vulnerability analysis and secure version recommendations.

## 🤖 Agent Orchestration and Loop Safety

*Multi-agent workflows, sub-agents, and automated loop security.*

- [claude-code-hooks-multi-agent-observability](https://github.com/disler/claude-code-hooks-multi-agent-observability) - Hook-based monitoring for multi-agent Claude Code sessions.
- [awesome-ai-agents-security](https://github.com/ProjectRecon/awesome-ai-agents-security) - Living map of the AI agent security ecosystem covering orchestration risks.
- [Microsoft Agent Governance Toolkit](https://github.com/microsoft/agent-governance-toolkit) - Zero-trust execution for multi-agent workflows with cross-agent policy enforcement.
- [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) - 2026 standard: agent goal hijacking, tool misuse, identity abuse, delegation risks.
- [NVIDIA Safety for Agentic AI](https://github.com/NVIDIA-AI-Blueprints/safety-for-agentic-ai) - Build/deploy/run safety patterns for agentic architectures.
- [Fortune: AI's Triple Act at Black Hat/DEF CON](https://fortune.com/2026/08/12/hacker-bodyguard-target-ais-triple-act-at-the-years-biggest-security-showdowns/) - Coverage of agent-to-agent interaction risks and shadow AI attack surfaces.

## 🖥️ OS and Endpoint Hardening

*Platform-specific security for Claude Code workstations.*

- [macOS Seatbelt Profiles](https://www.anthropic.com/engineering/claude-code-sandboxing) - How Claude Code uses Seatbelt for filesystem and network isolation on macOS.
- [Linux Bubblewrap Isolation](https://www.anthropic.com/engineering/claude-code-sandboxing) - Bubblewrap process isolation for Claude Code on Linux.
- [Sensitive File Deny Patterns](https://code.claude.com/docs/en/settings) - OS-appropriate deny rules for credential files, SSH keys, cloud configs.
- [VS Code Security Integration](https://code.claude.com/docs/en/vs-code) - Restricted Mode, trust verification, auto-edit risks, third-party provider controls.

## 🛠️ Security Tools and Scanners

*Tools for auditing, scanning, and testing Claude Code and its ecosystem.*

### Claude Code Specific

- [claude-code-security-review](https://github.com/anthropics/claude-code-security-review) - Official Anthropic GitHub Action for AI-powered security review of PRs.
- [Snyk agent-scan](https://github.com/snyk/agent-scan) - Professional scanner: AI agents, MCP servers, skills. Auto-discovers and validates across 15+ risk categories.
- [Trail of Bits Skills](https://github.com/trailofbits/skills) - Claude Code skills for security research, vulnerability detection, and audit workflows.
- [Claude Code Security Auditor](https://github.com/danielrosehill/Claude-Code-Security-Auditor) - Pattern for device-level security audits using Claude Code.

### MCP Scanners

- [mcp-scan (Invariant Labs)](https://github.com/invariantlabs-ai/mcp-scan) - MCP scanner with proxy mode for real-time connection monitoring.
- [Cisco MCP Scanner](https://github.com/cisco-ai-defense/mcp-scanner) - Enterprise-grade threat detection for MCP servers.
- [MCP Security Scanner (SARIF)](https://github.com/nostalgicskinco/mcp-security-scanner) - Static + dynamic analysis with GitHub code scanning integration.
- [AWS MCP Security Scanner](https://github.com/aws-samples/sample-mcp-security-scanner) - Integrates Checkov + Semgrep + Bandit via MCP server interface.

### LLM Security Toolkits

- [LLM Guard (Protect AI)](https://github.com/protectai/llm-guard) - Input/output validation, PII detection, toxicity filtering, secrets scanning. ~4k stars.
- [NeMo Guardrails (NVIDIA)](https://github.com/NVIDIA-NeMo/Guardrails) - Programmable guardrails with Colang for dialog flow control and vulnerability scanning. ~4.5k stars.
- [promptfoo](https://github.com/promptfoo/promptfoo) - Red-team LLM apps: adaptive attacks, CI/CD integration, declarative configs. ~6k stars.
- [Garak (NVIDIA)](https://github.com/NVIDIA/garak) - Generative AI red-teaming: 37+ probes, 23 backends, prompt injection to data extraction.
- [PyRIT (Microsoft)](https://github.com/Azure/PyRIT) - Enterprise red-teaming for generative AI in Azure environments.
- [Vigil](https://github.com/deadbits/vigil-llm) - Detect prompt injections, jailbreaks, and risky LLM inputs.
- [Langfuse Security & Guardrails](https://langfuse.com/docs/security-and-guardrails) - Observability platform with built-in security and guardrail integrations.

### Secrets Scanners

- [TruffleHog](https://github.com/trufflesecurity/trufflehog) - 800+ credential types with live verification. Scans Git, filesystems, cloud storage. ~18k stars.
- [Gitleaks](https://github.com/gitleaks/gitleaks) - Regex + entropy secrets detection. Fast, accurate, minimal false positives. ~19k stars.
- [ggshield (GitGuardian)](https://github.com/GitGuardian/ggshield) - 500+ secret types with pre-commit and CI integration.

## 🐛 Vulnerability Research and Disclosures

*Published CVEs, exploits, and security research on Claude Code.*

- [CVE-2025-59536: MCP Configuration RCE](https://research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files-cve-2025-59536/) - Check Point: remote code execution via malicious MCP configuration in `.claude/settings.json`.
- [CVE-2025-59356: Hooks-Based RCE](https://research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files-cve-2025-59536/) - Check Point: RCE through malicious hooks in project settings files.
- [CVE-2026-21852: API Key Harvesting](https://research.checkpoint.com/2026/rce-and-api-token-exfiltration-through-claude-code-project-files-cve-2025-59536/) - Check Point: API key extraction from Claude Code sessions via crafted project files.
- [Dark Reading: Flaws Put Developer Machines at Risk](https://www.darkreading.com/application-security/flaws-claude-code-developer-machines-risk) - Coverage of Check Point findings and implications for developer workstations.
- [The Hacker News: Claude Code RCE and Key Exfiltration](https://thehackernews.com/2026/02/claude-code-flaws-allow-remote-code.html) - Technical breakdown of exploitation chains.
- [SecurityWeek: Developer Devices Exposed](https://www.securityweek.com/claude-code-flaws-exposed-developer-devices-to-silent-hacking) - Analysis of silent attack vectors in Claude Code project files.
- [HackerOne: Report Claude Code Vulnerabilities](https://code.claude.com/docs/en/legal-and-compliance) - Official responsible disclosure channel.

## 📐 Frameworks and Standards

*Industry frameworks applicable to AI coding agent security.*

- [OWASP Top 10 for LLM Applications (2025)](https://owasp.org/www-project-top-10-for-large-language-model-applications/) - Industry standard for LLM security risks. Prompt injection is #1.
- [OWASP Top 10 for Agentic Applications (2026)](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) - Peer-reviewed by 100+ researchers: goal hijacking, tool misuse, identity abuse, supply chain.
- [OWASP AI Vulnerability Scoring System (AIVSS)](https://aivss.owasp.org/) - Standardized framework for scoring AI-specific security vulnerabilities.
- [OWASP AI Security Verification Standard (AISVS)](https://github.com/OWASP/AISVS) - Structured checklist for verifying AI application security.
- [OWASP AI Exchange](https://github.com/OWASP/www-project-ai-security-and-privacy-guide) - 300+ page reference on AI threats and controls.
- [MCP Server Security Standard](https://github.com/mcp-security-standard/mcp-server-security-standard) - Certification framework for MCP server security compliance.
- [NIST AI Risk Management Framework](https://www.nist.gov/artificial-intelligence/executive-order-safe-secure-and-trustworthy-artificial-intelligence) - Federal guidance on AI risk management.
- [MITRE ATLAS](https://atlas.mitre.org/) - Adversarial Threat Landscape for AI Systems — knowledge base of adversary tactics and techniques.
- [Agentic AI Top 10 Vulnerability (CSA/OWASP)](https://github.com/precize/Agentic-AI-Top10-Vulnerability) - Community documentation for OWASP/CSA red teaming work.

## 📚 Research, Talks, and Writeups

*High-quality security research, conference material, and technical analysis.*

### Conference Material

- [Black Hat USA 2025: AI Security Crossroads](https://www.wwt.com/blog/the-ai-security-crossroads-black-hat-and-defcon-2025-show-whats-next) - Comprehensive takeaways on agentic AI offense/defense.
- [DEF CON 33: AgentFlayer Attacks](https://www.csoonline.com/article/4037869/5-key-takeaways-from-black-hat-usa-2025.html) - 0-click attacks on enterprise AI assistants. 174 vulnerabilities reported, 22 CVEs.
- [Black Hat/DEF CON: AI Offense vs Defense](https://www.theregister.com/2025/08/11/ai_security_offense_defense) - Analysis: AI more useful for defense than hacking — but agent attacks are accelerating.

### Technical Research

- [Trail of Bits AI/ML Security](https://www.trailofbits.com/services/software-assurance/ai-ml/) - Professional AI security assessment methodology: root cause analysis over checklists.
- [Trail of Bits Publications](https://github.com/trailofbits/publications) - Archive of security research papers and presentations.
- [Trail of Bits awesome-ml-security](https://github.com/trailofbits/awesome-ml-security) - Curated ML security references, tools, and guidance.
- [LLM Security Guide](https://github.com/requie/LLMSecurityGuide) - Comprehensive reference: OWASP GenAI Top-10, prompt injection, real-world incidents, defense catalogs.
- [AI Red-Teaming Guide](https://github.com/requie/AI-Red-Teaming-Guide) - Adversarial testing and security evaluation methodology for AI systems.
- [Awesome LLMSecOps](https://github.com/wearetyomsmnv/Awesome-LLMSecOps) - LLM Security Operations: tools, frameworks, and operational guidance.

### Vendor Research

- [VentureBeat: Claude Code Security Wakeup Call](https://venturebeat.com/security/anthropic-claude-code-security-reasoning-vulnerability-hunting) - Industry impact analysis of Anthropic's security capabilities.
- [CSO Online: Industry Wakeup Call](https://www.csoonline.com/article/4136294/anthropics-claude-code-security-rollout-is-an-industry-wakeup-call.html) - Why Claude Code Security changes the AppSec landscape.
- [DataDome: MCP Prompt Injection Prevention](https://datadome.co/agent-trust-management/mcp-security-prompt-injection-prevention/) - Practical guide to stopping prompt injection in MCP deployments.
- [Lares: OWASP Agentic Top 10 in the Wild](https://labs.lares.com/owasp-agentic-top-10/) - Real-world threat examples mapped to OWASP Agentic categories.

## 🔄 Competitor and Adjacent Controls

*How other AI coding tools handle security — useful for comparison and gap analysis.*

- [GitHub Copilot Agent Control Plane](https://github.blog/changelog/2026-02-26-enterprise-ai-controls-agent-control-plane-now-generally-available/) - Enterprise AI controls: MCP allowlists, audit logs, RBAC, session monitoring. GA Feb 2026.
- [GitHub Agentic Security Principles](https://github.blog/ai-and-ml/github-copilot/how-githubs-agentic-security-principles-make-our-ai-agents-as-secure-as-possible/) - Autonomy limits, access controls, code scanning, agent governance.
- [Microsoft Agent Governance Toolkit](https://github.com/microsoft/agent-governance-toolkit) - Zero-trust agent framework: policy enforcement, identity, sandboxing.
- [Google MCP Security Servers](https://github.com/google/mcp-security) - Security Operations and Threat Intelligence MCP servers.
- [Contrast Security MCP](https://github.com/Contrast-Security-OSS/mcp-contrast) - Application security vendor MCP integration for vulnerability remediation.
- [Palo Alto + NeMo Guardrails](https://www.paloaltonetworks.com/blog/network-security/securing-genai-with-ai-runtime-security-and-nvidia-nemo-guardrails/) - AI Runtime Security integration with enterprise guardrails.

## ✅ Checklists and Templates

*Ready-to-use security checklists, policy templates, and configuration references.*

- [Trail of Bits claude-code-config](https://github.com/trailofbits/claude-code-config) - Production-ready config templates from security experts. Start here.
- [SlowMist MCP Security Checklist](https://github.com/slowmist/MCP-Security-Checklist) - Input validation, rate limiting, RBAC, credential management, container hardening.
- [MCP Server Security Standard](https://github.com/mcp-security-standard/mcp-server-security-standard) - Testable compliance checklist with evidence schemas.
- [OWASP AISVS Checklist](https://github.com/OWASP/AISVS) - Verification standard for AI application security.
- [claude-code-security](https://github.com/marc-shade/claude-code-security) - Progressive hardening checklist: agent config → hooks → runtime → injection → supply chain.
- [claude-code-safety-net Rules Reference](https://github.com/kenryu42/claude-code-safety-net/blob/main/CUSTOM_RULES_REFERENCE.md) - Custom rules reference for defining safe/dangerous command patterns.

## 🌐 Community and Ecosystem

*Related lists, communities, and ecosystem resources.*

- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) - Comprehensive Claude Code resource: skills, hooks, plugins, applications.
- [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security) - MCP security vulnerabilities, articles, and best practices. ~660 stars.
- [awesome-ai-agents-security](https://github.com/ProjectRecon/awesome-ai-agents-security) - Living map of the AI agent security landscape.
- [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) - LLM security tools, documents, and research.
- [awesome-ai-security](https://github.com/ottosulin/awesome-ai-security) - Broad AI security resources: offensive, defensive, governance.
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) - MCP server directory for the ecosystem.
- [awesome-claude-code-plugins](https://github.com/ccplugins/awesome-claude-code-plugins) - Curated Claude Code plugins list.
- [awesome-cybersecurity-agentic-ai](https://github.com/raphabot/awesome-cybersecurity-agentic-ai) - Cybersecurity + agentic AI resources.
- [Awesome LLM Agent Security](https://github.com/wearetyomsmnv/Awesome-LLM-agent-Security) - Agent-specific attacks, vulnerabilities, exploitation techniques.
- [awesome-ml-security (Trail of Bits)](https://github.com/trailofbits/awesome-ml-security) - ML security from a leading research firm.

---

## Star History

<a href="https://star-history.com/#efij/awesome-claude-code-security&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=efij/awesome-claude-code-security&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=efij/awesome-claude-code-security&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=efij/awesome-claude-code-security&type=Date" />
 </picture>
</a>

---

## Contributing

Contributions welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.

This is a **curated** list — quality over quantity. See the [inclusion criteria](CONTRIBUTING.md#inclusion-criteria) before submitting.

## License

[![CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

This work is licensed under a [Creative Commons Attribution 4.0 International License](LICENSE).
