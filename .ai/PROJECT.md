# Architect–Worker Project Contract

## Purpose

This repository demonstrates and supports a disciplined architect–worker development workflow. The architect defines bounded work and reviews outcomes; the worker implements exactly one task at a time.

## Repository

- Framework: Next.js 16 App Router
- Language: TypeScript with strict mode enabled
- Runtime UI: React 19
- Styling: Tailwind CSS 4 and shadcn components
- Package manager: pnpm 12.3.4
- Import alias: `@/*`
- Primary application directories: `app/`, `components/`, and `lib/`

## Roles

### Architect

- Owns architecture, contracts, task boundaries, and acceptance criteria.
- Writes the active task in `.ai/TASK.yaml`.
- Reviews the worker commit against the task and records durable decisions here or in `.ai/DECISIONS.md`.
- Dispatches correction tasks instead of silently expanding scope.

### Worker

- Starts from the task's `base_commit` on a dedicated branch.
- Changes only files allowed by `.ai/TASK.yaml`.
- Runs every required check and records evidence in `.ai/RESULT.yaml`.
- Stops and reports blockers instead of guessing or changing architecture.

## Invariants

1. Keep `main` deployable; implementation arrives through focused pull requests.
2. One task, one concern, and one worker commit per pull request unless the architect explicitly permits otherwise.
3. Do not add dependencies, modify schemas, or perform unrelated refactors unless the task explicitly allows it.
4. Preserve strict TypeScript, accessibility, security, and existing project conventions.
5. Never claim a check passed without recording its command and exit code.
6. Never commit secrets, environment-variable values, generated build output, or successful raw logs.
7. If actual repository conditions conflict with the task, stop and report the conflict.

## Standard workflow

1. Architect inspects the latest `main` and replaces `.ai/TASK.yaml` with one bounded task.
2. Worker creates `worker/<task-id>` from `base_commit`.
3. Worker implements, runs checks, writes `.ai/RESULT.yaml`, commits, pushes, and opens a pull request.
4. Architect reviews `base_commit..worker_commit` against the task.
5. The pull request is approved or a narrowly scoped correction task is issued.

## Default checks

Use checks that exist in `package.json`. This project currently supports:

```bash
pnpm build
```

Add lint, type-check, and test commands to a task only after the corresponding scripts exist. A task may also require targeted browser verification for user-visible behavior.

## Definition of done

A task is complete only when its acceptance criteria are met, required checks are recorded in `.ai/RESULT.yaml`, no undisclosed scope deviation exists, and the worker commit is ready for architect review.
