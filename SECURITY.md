# Security Policy

## Scope

TPMN-PSL is a **specification document**, not executable software. It defines notation, grammar, and protocol rules — it does not ship runnable code.

Security concerns relevant to this repository:

- **Specification vulnerabilities** — logical flaws in the protocol that could be exploited to produce misleading epistemic tags or bypass SPT checks
- **Supply chain** — tampering with the spec text, extension templates, or GitHub Pages content
- **Implementation guidance** — spec language that could lead implementers to build insecure systems

## Reporting

If you find a vulnerability in the specification logic or the repository infrastructure:

1. **Do not open a public issue.**
2. Use [GitHub's private vulnerability reporting](https://github.com/gem-squared/tpmn-psl/security/advisories/new) for this repository.
3. Include: affected spec section, the vulnerability, and potential impact.

We will acknowledge receipt within 7 days and provide a resolution timeline.

## Supported Versions

| Version | Supported |
|---------|-----------|
| v0.1.5-p | Yes      |
| < v0.1.5-p | No    |
