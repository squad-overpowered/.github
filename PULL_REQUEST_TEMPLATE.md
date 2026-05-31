## Type of change

<!-- Mark the relevant option with an [x] -->

- [ ] `feat` — New feature
- [ ] `fix` — Bug fix
- [ ] `refactor` — Code change that neither fixes a bug nor adds a feature
- [ ] `perf` — Performance improvement
- [ ] `test` — Adding or updating tests
- [ ] `docs` — Documentation only
- [ ] `build` — Build system or dependency changes
- [ ] `ci` — CI/CD changes
- [ ] `chore` — Other changes

## Description

<!-- What does this PR do? Link to the issue it resolves. -->

Closes #

## Changes

<!-- List the key changes made in this PR. -->

-
-
-

## Checklist

### General
- [ ] Code compiles without errors (`npx nx affected -t build`)
- [ ] All tests pass (`npx nx affected -t test`)
- [ ] Lint passes (`npx nx affected -t lint`)
- [ ] No sensitive data (secrets, credentials, PII) committed

### Frontend (if applicable)
- [ ] Component uses `ChangeDetectionStrategy.OnPush`
- [ ] Standalone component with `inject()` pattern (no constructor DI)
- [ ] Uses Angular signals (`input()`, `output()`, `computed()`) where appropriate
- [ ] Follows vibeSquad design system (Tailwind + DaisyUI, no inline styles)
- [ ] Responsive — tested at mobile (375px), tablet (768px), desktop (1280px)
- [ ] Accessible — correct ARIA roles, keyboard navigable, sufficient color contrast
- [ ] Component style budget respected (< 6kB per component)

### Backend (if applicable)
- [ ] DTOs validated with `class-validator`
- [ ] Sensitive endpoints protected by auth guard
- [ ] No raw SQL — uses TypeORM query builder or repository pattern
- [ ] Database migrations created for schema changes
- [ ] API responses follow existing response shape conventions

### Tests
- [ ] Unit tests added or updated for changed logic
- [ ] Edge cases and error paths covered

## Screenshots / recordings

<!-- For UI changes, attach before/after screenshots or a short screen recording. -->

## Notes for reviewers

<!-- Anything the reviewer should pay special attention to. -->
