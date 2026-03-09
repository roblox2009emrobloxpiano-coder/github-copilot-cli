# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| Latest  | :white_check_mark: |
| < Latest| :x:                |

We recommend always using the latest release.

## Reporting a Vulnerability

We take the security of github-copilot-cli seriously. If you discover a security vulnerability, please follow these steps:

### How to Report

**Please do NOT report security vulnerabilities through public GitHub issues.**

Instead:

1. **Preferred**: Use GitHub's Security Advisory feature
   - Go to the [Security tab](https://github.com/trsdn/github-copilot-cli/security)
   - Click "Report a vulnerability"
   - Fill out the form with details

### What to Include

- **Description** of the vulnerability
- **Steps to reproduce** the issue
- **Potential impact** of the vulnerability
- **Suggested fix** (if you have one)

### What to Expect

1. **Acknowledgment**: Within 48 hours
2. **Assessment**: We'll determine severity
3. **Fix Timeline**: Critical (7 days), High (14 days), Medium (30 days), Low (next release)

## Security Best Practices

### For Users

1. **Review generated code** before executing it
2. **Don't trust untrusted sources** when copying customizations
3. **Keep Copilot CLI updated** (`/update` or reinstall)
4. **Use explicit tool lists** in agent definitions (`tools: [...]`)
5. **Review tool approval requests** — don't blindly approve all tools
6. **Be cautious with `--allow-all` / `--yolo`** flags in untrusted repos

### For Agent Authors

1. **Minimize tool access** — use explicit `tools: []` instead of all tools
2. **Validate tool output** — treat all tool output as untrusted
3. **Avoid destructive commands** — prefer safe, narrowly-scoped operations
4. **Document security implications** in agent and skill descriptions
5. **Test in isolated environments** before sharing agents

## Resources

- [GitHub Security Advisories](https://github.com/trsdn/github-copilot-cli/security/advisories)
- [Copilot CLI Security Docs](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli)
- [Contributing Guidelines](CONTRIBUTING.md)

Thank you for helping keep github-copilot-cli secure! 🔒
