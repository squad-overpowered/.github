# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| latest (main branch) | ✅ |
| develop branch | ✅ (pre-release) |
| older releases | ❌ |

---

## Reporting a Vulnerability

**Do not report security vulnerabilities through public GitHub issues.**

If you discover a security vulnerability in Squad Overpowered, please report it responsibly:

### How to Report

1. **Email**: Send a detailed report to the security contact listed in the organization's private contact page, or open a [GitHub Security Advisory](https://docs.github.com/en/code-security/security-advisories/working-with-repository-security-advisories/creating-a-repository-security-advisory) in the affected repository.

2. **Include in your report**:
   - Type of vulnerability (e.g., XSS, SQL Injection, authentication bypass)
   - Affected component (frontend, backend, specific module)
   - Step-by-step instructions to reproduce
   - Potential impact and attack scenario
   - Suggested fix (optional but appreciated)

### What to Expect

- **Acknowledgement**: Within 48 hours
- **Initial assessment**: Within 5 business days
- **Fix timeline**: Depends on severity (see below)
- **Credit**: We'll credit you in the release notes if you wish

---

## Severity Levels & Response Times

| Severity | Examples | Target fix time |
|---|---|---|
| **Critical** | Authentication bypass, RCE, data breach | 24–72 hours |
| **High** | Privilege escalation, SQL injection, stored XSS | 1–2 weeks |
| **Medium** | Reflected XSS, CSRF, sensitive data exposure | 2–4 weeks |
| **Low** | Information disclosure, minor misconfigurations | Next release |

---

## Security Scope

### In scope
- Angular frontend (`apps/frontend/`)
- NestJS REST API (`apps/backend/`)
- Authentication and authorization flows (JWT, OAuth)
- Database queries and ORM usage
- API input validation and sanitization
- File upload handling
- Third-party dependency vulnerabilities

### Out of scope
- Vulnerabilities in third-party services we depend on (report to them directly)
- Social engineering attacks
- Physical security
- DoS/DDoS attacks
- Issues requiring physical access to a user's device

---

## Security Best Practices for Contributors

When contributing code, please follow these guidelines:

- **Never commit secrets** — use environment variables. The `.env` file is gitignored.
- **Validate all input** at the API boundary using `class-validator` DTOs.
- **Use parameterized queries** via TypeORM — never string-concatenated SQL.
- **Protect sensitive routes** with `@UseGuards(JwtAuthGuard)`.
- **Sanitize user-generated content** before rendering in templates.
- **Follow OWASP Top 10** guidelines when writing backend code.
- Run `npm audit` before submitting PRs with dependency changes.

---

## Known Security Configurations

- JWT tokens expire after 1 hour (access) / 7 days (refresh)
- Passwords are hashed with bcrypt (minimum 10 rounds)
- CORS is configured to allow only trusted origins
- Rate limiting is applied to authentication endpoints
