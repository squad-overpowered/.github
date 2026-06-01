# Squad Overpowered — `.github`

This repository contains organization-level configuration for the **Squad Overpowered** GitHub organization: community health files, issue templates, CI/CD workflows, and the organization profile page.

---

## Structure

```
.github/
├── profile/
│   └── README.md              <- Organization profile (shown on github.com/squad-overpowered)
├── ISSUE_TEMPLATE/            <- Bug report and feature request templates
├── workflows/                 <- GitHub Actions workflows
├── CONTRIBUTING.md            <- Contribution guidelines
├── CODE_OF_CONDUCT.md         <- Community standards
├── SECURITY.md                <- Vulnerability reporting policy
└── PULL_REQUEST_TEMPLATE.md   <- PR checklist
```

---

## Workflows

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| `release.yml` | Push to `master` | Automated versioning and changelog via release-please |
| `dependency-audit.yml` | Weekly | Security audit of dependencies |
| `stale.yml` | Daily | Close stale issues and PRs |

---

## Community Files

Files in this repo automatically apply to all repositories in the organization that do not have their own copy:

- `CODE_OF_CONDUCT.md`
- `CONTRIBUTING.md`
- `SECURITY.md`
- `PULL_REQUEST_TEMPLATE.md`
- `ISSUE_TEMPLATE/`