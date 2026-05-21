# Input Validation Rule

입력 파일은 코드 생성 전에 검증한다.
Empty required values stop generation and must be reported as a checklist.

## Split Input

Validate split input files before code generation.
If `input/index.md` is missing, stop generation and request or create the split input file set.

Required split files: `input/project.md`, `input/stack.md`, `input/design.md`, `input/api.md`, `input/auth.md`, and `input/resource-manifest.md` before materialization or at least one file in `input/resources` after materialization.

## Required Fields

- Project: `name`, `type`, `defaultLanguage`, `supportedLanguages`.
- Stack/design: `versions`, `tableLibrary`, `uiKit`, `uiKitSource`, `uiKitProvider`, `primaryColor`, `font`, `density`.
- API/auth: `baseUrlEnv`, `authType`, `tokenStorage`, `permissionType`, `routes.signIn`, `routes.signUp`, `routes.afterSignIn`, `routes.afterSignOut`, `actions`.
- Resource: `label`, `entityName`, `route`, `listApi`, `navigation.category`, `navigation.order`, `pagination`, `defaultPageSize`, and at least one column with `key`, `label`, `type`.

## Resource Identity

In split mode, validate the resource identifier from the `resource:` field inside each file in `input/resources`.
The `resource:` field must match the filename `input/resources/{resource}.md`.

## Conditional Rules

- Validate conditional UI kit values according to `rules/ui-kit.md`.
- Validate optional CRUD fields according to `rules/crud-generation.md`.
- `swaggerUrl` is optional. OpenAPI and fallback behavior follows `workflow/05-openapi.md` and `rules/mock-data-fallback.md`.
- Auth is always generated for admin shells. Do not require auth API endpoint values when `swaggerUrl` is empty.
- If auth `mock.seedUsers` is empty and `swaggerUrl` is empty or unavailable, generate one synthetic admin seed user instead of stopping generation.
- If resource mock fallback is enabled with `storeBoundary: msw`, then `optionalTools.msw` must be true.
- If `swaggerUrl` is empty or unavailable and MSW is disabled for an MSW-bound resource fallback, stop generation and ask the user to enable MSW or provide a real API.
- Auth fallback may use a client-side adapter when MSW is disabled.

## Optional Fields

`swaggerUrl`, `secondaryColor`, `styleTokens`, `uiKitTheme`, `devServer`, `defaultSort`, `rowIdField`, `search`, `filters`.
