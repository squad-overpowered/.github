# Squad Overpowered — GitHub Copilot Workspace

This repository configures the **GitHub Copilot agent ecosystem** for the Squad Overpowered project. It contains custom agents, reusable prompt templates, and the organization profile page.

---

## Structure

```
.github/
├── profile/
│   └── README.md              ← Organization profile page (shown on GitHub org page)
├── agents/
│   ├── architect.agent.md
│   ├── analyst.agent.md
│   ├── designer.agent.md
│   ├── frontend-dev.agent.md
│   ├── backend-dev.agent.md
│   ├── tester.agent.md
│   └── devops.agent.md
└── prompts/
    ├── analyze-feature.prompt.md
    ├── new-angular-component.prompt.md
    ├── new-nestjs-module.prompt.md
    ├── write-tests.prompt.md
    ├── design-component.prompt.md
    └── review-code.prompt.md
```

---

## Agents

Custom agents are specialized Copilot personas with role-specific knowledge, tools, and conventions baked in. Select them from the agent picker in VS Code Copilot Chat.

### `@Architect`
**When to use**: Designing modules, defining API contracts, making technology decisions, planning database schemas, evaluating libraries, or reviewing architectural trade-offs.

Knows: Nx monorepo structure, lib boundaries, TypeORM schema design, shared-types conventions, ADR format.

---

### `@Analyst`
**When to use**: Breaking down a feature request into tasks, mapping user stories to code, identifying edge cases, or creating ordered implementation plans before development starts.

Knows: Domain entities (Player, Squad, Formation, User), feature/module structure, frontend+backend split.

---

### `@UI Designer`
**When to use**: Designing new components, working with the design system, reviewing visual consistency, building responsive layouts, or specifying animations.

Knows: vibeSquad theme (`#4ADE80` / `#0A0A0A`), Tailwind CSS 3, DaisyUI 4, Lottie animations, SCSS token system, Angular component budget limits.

---

### `@Frontend Dev`
**When to use**: Creating or modifying Angular components, services, pipes, routes, or any code inside `apps/frontend`.

Knows: Angular 21 zoneless + signals, `ChangeDetectionStrategy.OnPush`, standalone components, `input()` / `output()` signals, `@if` / `@for` control flow, `inject()` pattern, path aliases.

---

### `@Backend Dev`
**When to use**: Creating or modifying NestJS modules, controllers, services, TypeORM entities, DTOs, guards, or database migrations in `apps/backend`.

Knows: NestJS modular architecture, TypeORM + PostgreSQL, class-validator DTOs, JWT + OAuth guards, API versioning, migration workflow.

---

### `@Tester`
**When to use**: Writing unit tests with Jest, component tests, or end-to-end tests with Playwright. Also for reviewing test coverage or testing strategies.

Knows: Angular TestBed + `provideZonelessChangeDetection()`, `@testing-library/angular`, NestJS `Test.createTestingModule()`, Playwright page object patterns, coverage targets.

---

### `@DevOps`
**When to use**: Setting up Docker, CI/CD pipelines, GitHub Actions workflows, environment configuration, database provisioning, or production deployment.

Knows: Nx affected commands, multi-stage Docker builds, GitHub Actions for monorepos, environment variable management, deployment checklist.

---

## Prompts

Prompts are reusable task templates. Type `/` in Copilot Chat to access them.

### `/analyze-feature`
Analyze a feature request and produce a complete implementation plan with tasks ordered by dependency, edge cases, and acceptance criteria — split across frontend, backend, and shared libs.

**Usage**: `/analyze-feature add player search with filters to the squad builder`

---

### `/new-angular-component`
Scaffold a new standalone Angular component with its `.ts`, `.html`, `.scss`, and `.spec.ts` files following project conventions (OnPush, signals, DaisyUI).

**Usage**: `/new-angular-component player-stats-overlay in squad-builder feature`

---

### `/new-nestjs-module`
Scaffold a full NestJS feature module: entity, DTOs, service, controller, module file, and spec files. Registers it in `app.module.ts`.

**Usage**: `/new-nestjs-module squads — manages user squad creation and persistence`

---

### `/write-tests`
Write Jest unit tests or Playwright e2e tests for a given file or feature. Follows project test patterns and coverage targets.

**Usage**: `/write-tests apps/backend/src/modules/players/players.service.ts`

---

### `/design-component`
Design a UI component using the vibeSquad design system. Outputs HTML template, Tailwind/DaisyUI classes, SCSS, responsive notes, and accessibility details.

**Usage**: `/design-component formation grid showing 11 player slots in a 4-3-3 layout`

---

### `/review-code`
Review code changes for correctness, security (OWASP Top 10), Angular/NestJS conventions, and test coverage. Returns findings with severity levels and a final verdict.

**Usage**: `/review-code apps/backend/src/modules/auth/`

---

## Recommended Workflow

```
Feature request
      │
      ▼
 /analyze-feature         ← break it down first
      │
      ├──► @Architect      ← if design decisions are needed
      ├──► @UI Designer    ← if UI needs designing first
      │
      ▼
 @Frontend Dev             ← implement Angular side
 /new-angular-component
      │
 @Backend Dev              ← implement NestJS side
 /new-nestjs-module
      │
      ▼
 @Tester                   ← write tests
 /write-tests
      │
      ▼
 /review-code              ← review before merging
      │
      ▼
 @DevOps                   ← deploy
```
