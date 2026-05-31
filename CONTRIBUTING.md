# Contributing to Squad Overpowered

Thanks for contributing! This guide covers everything you need to get the project running locally and contribute effectively.

---

## Prerequisites

| Tool | Version | Install |
|------|---------|---------|
| Node.js | 24.x | [nodejs.org](https://nodejs.org) |
| npm | 11.x | Included with Node |
| Git | latest | [git-scm.com](https://git-scm.com) |
| PostgreSQL | 16+ | [postgresql.org](https://www.postgresql.org) |

---

## Local Setup

### 1. Clone the monorepo

```bash
git clone https://github.com/squad-overpowered/squad-overpowered.git
cd squad-overpowered
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

```bash
# Backend
cp apps/backend/.env.example apps/backend/.env
# Edit apps/backend/.env with your local PostgreSQL credentials
```

Required variables:
```env
DATABASE_URL=postgresql://postgres:password@localhost:5432/squad_overpowered
JWT_SECRET=your-local-dev-secret
JWT_REFRESH_SECRET=your-local-refresh-secret
NODE_ENV=development
```

### 4. Run database migrations

```bash
npx nx run backend:migration:run
```

### 5. Start the development servers

```bash
# Frontend (Angular) — http://localhost:4200
npx nx serve frontend

# Backend (NestJS) — http://localhost:3000
npx nx serve backend

# Both at once
npx nx run-many -t serve --projects=frontend,backend
```

---

## Monorepo Structure

```
squad-overpowered/
├── apps/
│   ├── frontend/        ← Angular 21 app (zoneless, signals, standalone)
│   ├── backend/         ← NestJS REST API
│   ├── frontend-e2e/    ← Playwright e2e tests
│   └── backend-e2e/     ← API e2e tests
├── libs/
│   ├── shared-types/    ← TypeScript interfaces and enums (Player, Squad, User…)
│   ├── shared-utils/    ← Pure utility functions shared across apps
│   └── api-interfaces/  ← Request/response contracts (DTOs)
└── .github/             ← Copilot agents, prompts, workflows
```

**Import rule**: Apps can import from libs. Libs cannot import from apps. Libs can import from other libs only if there is no circular dependency.

```typescript
// ✅ OK
import { Player } from '@squad-overpowered/shared-types';

// ❌ Not allowed
import { something } from 'apps/frontend/src/...';
```

---

## Branch Workflow

```
main          ← production (protected, requires PR + 1 approval)
  └── develop ← integration branch (protected, requires PR)
        └── feature/your-feature-name
        └── fix/your-bug-fix
        └── refactor/your-refactor
```

1. Branch off `develop`, never off `main`
2. Open a PR into `develop` when ready
3. `develop` → `main` is merged periodically for releases

---

## Commit Convention

We use **Conventional Commits**. Every commit must follow this format:

```
<type>[optional scope]: <description>
```

| Type | When to use |
|------|-------------|
| `feat` | New feature visible to users |
| `fix` | Bug fix |
| `refactor` | Code change without behavior change |
| `perf` | Performance improvement |
| `test` | Adding or fixing tests |
| `docs` | Documentation only |
| `build` | Dependency or build config changes |
| `ci` | CI/CD workflow changes |
| `chore` | Maintenance, tooling |

**Examples:**
```bash
feat(squad-builder): add drag-and-drop player positioning
fix(auth): resolve token refresh race condition
test(players): add unit tests for player search service
refactor(ui): extract player card into shared component
```

Rules:
- Imperative mood: "add" not "added"
- Lowercase after the colon
- No period at the end
- Subject < 50 characters

---

## Running Tests

```bash
# Unit tests (all)
npx nx run-many -t test

# Unit tests (only affected by your changes)
npx nx affected -t test

# Unit tests with coverage
npx nx affected -t test --coverage

# E2e tests (frontend)
npx nx e2e frontend-e2e

# E2e tests (backend)
npx nx e2e backend-e2e
```

Coverage targets: **> 80%** for services, **> 60%** for components.

---

## Linting & Formatting

```bash
# Lint (all)
npx nx run-many -t lint

# Lint (affected)
npx nx affected -t lint

# Fix lint issues automatically
npx nx affected -t lint --fix
```

---

## Code Conventions

### Angular
- Standalone components with `ChangeDetectionStrategy.OnPush`
- Use `inject()` — no constructor injection
- Use signals: `signal()`, `computed()`, `effect()`, `input()`, `output()`
- Control flow: `@if`, `@for`, `@switch` — never `*ngIf` / `*ngFor`
- Always import design tokens: `@use '../../../../styles/tokens' as tokens;`

### NestJS
- Feature module per domain: `modules/players/`, `modules/squads/`, etc.
- DTOs with `class-validator` decorators
- TypeORM repository pattern — no raw SQL
- Protect sensitive endpoints with `@UseGuards(JwtAuthGuard)`

### Shared libs
- `shared-types`: interfaces and enums only — no runtime logic
- `shared-utils`: pure functions only — no Angular or NestJS imports
- `api-interfaces`: request/response DTO shapes only

---

## Using Copilot Agents & Prompts

The `.github/` repo includes custom agents and prompts that accelerate development. In VS Code Copilot Chat:

| Task | Tool |
|------|------|
| Break down a feature | `/analyze-feature` |
| Create Angular component | `/new-angular-component` |
| Create NestJS module | `/new-nestjs-module` |
| Write tests | `/write-tests` |
| Design a UI component | `/design-component` |
| Review code | `/review-code` |
| Architecture decisions | `@Architect` |
| UI/UX questions | `@UI Designer` |
| Angular help | `@Frontend Dev` |
| NestJS help | `@Backend Dev` |
| Testing strategy | `@Tester` |
| Deployment help | `@DevOps` |

---

## Pull Request Checklist

Before opening a PR:
- [ ] `npx nx affected -t build` — compiles without errors
- [ ] `npx nx affected -t test` — all tests pass
- [ ] `npx nx affected -t lint` — no lint errors
- [ ] No secrets committed
- [ ] PR description follows the template (auto-loaded when you open a PR)
- [ ] Commit messages follow Conventional Commits

---

## Getting Help

- Check existing issues before opening a new one
- Use the issue templates — they help us triage faster
- For questions about architecture or conventions, open a Discussion
- For security issues, see [SECURITY.md](SECURITY.md) — do not open public issues
