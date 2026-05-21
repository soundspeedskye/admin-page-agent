# Web Admin Page Agent Guide

이 폴더는 React 기반 admin 웹앱을 생성하는 에이전트 지침이다. 최종 산출물은 단순 골격이 아니라, 사용자가 바로 실행하고 이후 디테일을 수정할 수 있는 기본 구동 앱이어야 한다.

## Required Outcome

- A single full run must produce a runnable admin web app from `input/*`.
- The app must include working auth, private routing, sidebar navigation, generated resource pages, list tables, CRUD flows according to resource settings, typed API boundaries, and mock fallback when real APIs are unavailable.
- If Swagger/OpenAPI is unavailable or incomplete, mock fallback must make auth and resource screens usable without a backend.
- Mock resource rows must be visually rendered in generated list tables before completion.
- Basic sign-in, sign-up when enabled, sign-out, session restore or guard redirect, and private-route protection must work.
- Generated code must be a practical starting point for user customization, not a disposable scaffold.

## Run Order

- Validate split input through `input/index.md` and `rules/input-validation.md`.
- If required input is missing, stop and report a focused checklist before generation.
- Read baseline docs before workflow execution: `00-project-structure.md`, `01-package-baseline.md`, `02-typescript-baseline.md`, `03-vite-baseline.md`, and `04-format-lint.md`.
- Execute `workflow/00-bootstrap-project.md` through `workflow/09-review-and-verify.md` in order.
- Each workflow owns its required `rules/*.md`; read relevant rules before generating code.
- If dependency installation is needed, show the package manager and package list, then ask for approval before installing.

## Source Of Truth

- Project-specific values come only from `input/*`.
- Resource source of truth, `resource-index.json`, manifest usage, and token-budgeted resource reads follow `workflow/03-materialize-resources.md`, `workflow/04-navigation-map.md`, `workflow/06-resource-plan.md`, and `workflow/08-generate-list-pages.md`.
- Existing user code must be read before editing and must not be overwritten blindly.

## Generation Principles

- Follow FSD layer ownership.
- Keep DTO, schema, API, hook, UI, mapper, and mutation responsibilities separate.
- Keep the first chosen project structure and shared component usage consistent across later resources.
- Use the selected stack from `input/stack.md`; do not invent unrequested frameworks or libraries.
- Reuse verified core artifacts according to `rules/ui-core.md`.
- Keep common UI reusable through `shared/ui/lib` and `shared/ui/core`.
- Do not create `.mjs` repo artifacts. Temporary ESM execution should use `node --input-type=module`; temporary files, if unavoidable, must live outside the repo and be removed.

## Output

- Generate app code, config, verification results, and requested reports only.
- Routes, navigation, list pages, auth, query hooks, mutations, forms, mock fallback, table behavior, and UI wrappers follow their workflow/rule files.
- Generated resource pages must include page header, search/filter controls when configured, table, pagination, loading, empty, and error states.
- Generated CRUD pages must exist only for enabled CRUD actions and must use mock fallback operations when real API operations are unavailable.
- Generated auth pages must use configured auth routes and token/session storage rules.
- API modules must use the typed request boundary and must not import mock infrastructure directly.

## Completion

- Run lint.
- Run typecheck or build.
- Run runtime list smoke when generated list pages or mock fallback exist.
- Runtime list smoke must fail if mock row count is greater than 0 but no table row/cell is rendered.
- Verify basic auth fallback flow when Swagger/OpenAPI auth is unavailable.
- Fix failures before reporting completion.
