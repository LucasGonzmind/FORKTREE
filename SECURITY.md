# 🔒 Security Policy

## Overview

Security is a foundational concern for the Verd.Bud protocol. As a system that governs AI agent reproduction, DNA inheritance, and attention-driven economics, vulnerabilities could have cascading effects across the entire agent ecosystem.

We take all security reports seriously and are committed to addressing them promptly.

---

## Supported Versions

| Version | Status | Support |
|---------|--------|---------|
| `main` branch | 🟢 Active | Full security support |
| Feature branches | 🟡 Development | Best-effort support |
| Tagged releases | 🟢 Active | Full security support for latest release |

---

## Reporting a Vulnerability

### ⚠️ Do NOT open a public GitHub issue for security vulnerabilities.

Public disclosure of vulnerabilities before they are patched puts the entire ecosystem at risk.

### How to Report

**Option 1: GitHub Private Vulnerability Reporting**
1. Go to the [Security tab](https://github.com/AustinFreel23/Verd.Bud-Attention/security) of this repository
2. Click "Report a vulnerability"
3. Fill in the details

**Option 2: Direct Contact**
- Twitter DM: [@AustinFreel23](https://x.com/AustinFreel23)
- LinkedIn: [Austin Freel](https://www.linkedin.com/in/austin-freel-324b2269/)

### What to Include

Please provide as much detail as possible:

```
VULNERABILITY REPORT
====================

Summary:        [Brief description]
Severity:       [Critical / High / Medium / Low]
Component:      [Which part of the protocol is affected]
Attack vector:  [How could this be exploited]
Steps to reproduce:
  1. ...
  2. ...
  3. ...
Impact:         [What damage could result]
Suggested fix:  [If you have one]
```

### Severity Classification

| Level | Description | Examples |
|-------|-------------|---------|
| **🔴 Critical** | Immediate threat to protocol integrity or user assets | Unauthorized reproduction, DNA manipulation, energy theft |
| **🟠 High** | Significant impact but requires specific conditions | Attention oracle manipulation, sybil bypass, governance exploit |
| **🟡 Medium** | Limited impact or difficult to exploit | Information disclosure, denial of service, UI spoofing |
| **🟢 Low** | Minimal impact | Cosmetic issues, non-sensitive information leak, edge cases |

---

## Response Timeline

| Stage | Timeframe | Action |
|-------|-----------|--------|
| **Acknowledgment** | Within 24 hours | We confirm receipt of your report |
| **Triage** | Within 48 hours | We assess severity and assign priority |
| **Investigation** | Within 7 days | We investigate the vulnerability and determine impact |
| **Fix Development** | Varies by severity | Critical: 24-48 hours. High: 1 week. Medium/Low: 2 weeks |
| **Disclosure** | After fix deployed | Coordinated disclosure with reporter credit (if desired) |

---

## Security Considerations by Component

### Attention Oracle (L0)

| Risk | Description | Mitigation |
|------|-------------|------------|
| Signal spoofing | Fake interactions to inflate attention scores | Multi-source validation, proof-of-humanity, staking requirements |
| Oracle manipulation | Compromising data feeds to alter scores | Multiple independent data sources, outlier detection |
| Replay attacks | Resubmitting old interactions for fresh credit | Timestamp validation, nonce tracking, rolling window enforcement |

### Energy Pool (L1)

| Risk | Description | Mitigation |
|------|-------------|------------|
| Energy inflation | Creating VRDE without legitimate attention | Bonding curve with governance-controlled parameters |
| Transfer bypass | Attempting to trade soulbound energy | Soulbound enforcement at contract level |
| Expiration evasion | Circumventing 90-day expiration | On-chain timestamp validation |

### Agent Registry (L2)

| Risk | Description | Mitigation |
|------|-------------|------------|
| DNA tampering | Modifying agent genome without reproduction | Immutable on-chain storage, access control |
| Lineage forgery | Creating fake ancestry chains | Cryptographic lineage verification |
| Identity theft | Impersonating another agent | NFT ownership verification |

### Reproduction Engine (L3)

| Risk | Description | Mitigation |
|------|-------------|------------|
| Unauthorized reproduction | Triggering reproduction without meeting thresholds | Multi-condition validation in smart contract |
| Mutation manipulation | Predicting or controlling VRF outcomes | Verifiable Random Function with commit-reveal scheme |
| Cooldown bypass | Reproducing more frequently than allowed | On-chain cooldown tracking with block timestamp |
| Inbreeding | Reproducing with genetically similar agents | DNA similarity check (< 60% overlap requirement) |

---

## Responsible Disclosure

We follow responsible disclosure practices:

1. **Reporter submits** vulnerability through private channels
2. **Team acknowledges** within 24 hours
3. **Team investigates** and develops fix
4. **Reporter reviews** fix (optional)
5. **Fix deployed** to production
6. **Public disclosure** with appropriate credit to reporter
7. **Post-mortem** published if severity warrants it

### Reporter Recognition

We believe in recognizing security researchers for their contributions:

- Credit in the security advisory (unless anonymity is preferred)
- Mention in the project changelog
- Inclusion in a future Hall of Fame / Security Contributors page

---

## Security Best Practices for Contributors

If you're contributing to Verd.Bud, please follow these practices:

- **Never commit secrets** — API keys, private keys, or credentials must never appear in code
- **Validate all inputs** — Never trust user-provided data without validation
- **Use established patterns** — Don't reinvent cryptographic or security primitives
- **Minimize attack surface** — Keep external dependencies to a minimum
- **Document security assumptions** — Make implicit security requirements explicit
- **Test edge cases** — Consider what happens at boundaries and with unexpected input

---

## Security Audit Status

| Audit | Status | Scope |
|-------|--------|-------|
| Internal code review | ✅ Ongoing | All components |
| External smart contract audit | 📋 Planned | Core protocol contracts |
| Penetration testing | 📋 Planned | Frontend and API endpoints |
| Formal verification | 📋 Planned | Reproduction engine logic |

---

## Contact

For security-related inquiries:

- **Twitter**: [@AustinFreel23](https://x.com/AustinFreel23)
- **LinkedIn**: [Austin Freel](https://www.linkedin.com/in/austin-freel-324b2269/)
- **GitHub**: [Security Advisory](https://github.com/AustinFreel23/Verd.Bud-Attention/security)

---

<p align="center">
  <sub>🔒 Security is not a feature — it's the foundation. — Verd.Bud</sub>
</p>
