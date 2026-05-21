# 09 Review And Verify

생성 결과가 입력값과 규칙을 모두 만족하는지 확인한다.

## Input Review

- split input references resolve from `input/index.md`.
- resource files exist for the requested generation scope after materialization.
- no existing resource file was overwritten by materialization.
- existing resource files were changed only through an explicit diff-based update.
- workflows after materialization did not read `input/resource-manifest.md`.
- mock fallback report is present when Swagger/OpenAPI is unavailable.
- auth fallback report is present when Swagger/OpenAPI is unavailable or auth operations are not extracted.
- MSW handlers are generated only when `optionalTools.msw` is true.
- CRUD files are generated only for enabled resource CRUD actions.

## Checklist

- Every materialized resource file maps to one route and navigation child.
- Every route has a page component.
- Public sign-in and sign-up routes exist outside `PrivateLayout`.
- Private routes are guarded before page rendering.
- Sign-in stores token/session and redirects to `input/auth.md` `routes.afterSignIn`.
- Sign-out clears token/session and redirects to `input/auth.md` `routes.afterSignOut`.
- 401 responses clear auth storage and redirect to sign-in.
- Mock auth fallback can sign in with the configured seed user.
- Mock sign-up rejects duplicate email addresses.
- Every resource has API, query key, query hook.
- Every list page has table and pagination.
- Search and filters match split input files.
- Table columns match input order.
- Sidebar active state works.
- TypeScript aliases are consistent.
- No project-specific value remains in workflow docs.

## Runtime List Smoke

빌드 성공만으로 완료를 판단하지 않는다. mock fallback 또는 generated list page가
있는 경우 대표 private list route 하나를 실제 브라우저에서 확인한다.

- Start the dev server only after lint/typecheck/build pass.
- Sign in with the configured mock seed user when mock auth fallback is active.
- Open one representative generated list route, preferably the first private navigation child with mock rows.
- Assert there are no browser console errors.
- Assert the list count text is visible.
- If the source mock row count is greater than 0, assert the rendered table has at least one visible row or cell.
- Keep smoke output compact: route, console error count, list count text, rendered row count, and first visible row text only.
- Do not run create/update/delete smoke by default; run mutation smoke only when mutation files changed or the user explicitly asks for it.
- Do not dump full page HTML or screenshots unless the smoke check fails.

## Promote Verified Core Artifacts

runtime list smoke를 통과한 뒤에만 관련 `shared/ui/core` artifact를 baseline으로
승격한다. 실패한 artifact는 다음 실행에서 재사용 가능한 baseline으로 기록하지 않는다.

- Use `rules/ui-core.md` `Verified Core Artifact Baseline` as the source of truth for manifest schema, matching criteria, and reuse rules.
- Promote only artifacts that were exercised by the smoke route, such as `Table`, `Pagination`, `PageHeader`, and search panel wrappers on a generated list page.
- Do not include full source code, screenshots, or page HTML in `reports/core-artifacts.json`.

## Commands

- Run lint.
- Run typecheck or build.
- Run runtime list smoke when a generated list page or mock fallback is present.
- Run relevant tests if present.

Failures must be fixed before claiming completion.
