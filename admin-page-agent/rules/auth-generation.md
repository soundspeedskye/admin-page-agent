# Auth Generation Rule

admin 앱은 auth를 기본 골격으로 생성한다.
별도 auth mode를 두지 않고 `input/api.md`의 `swaggerUrl` 유무와 OpenAPI 추출 결과로 실제 API 또는 mock fallback을 결정한다.

## Read

- `input/auth.md`
- `input/api.md`
- `input/stack.md`
- `input/defaults/mock.md`
- `rules/auth-token-storage.md`
- `rules/private-route-guard.md`
- `rules/form-zod.md`
- `rules/mutation.md`
- `rules/error-feedback.md`

## Required Auth Surface

- public sign-in route.
- public sign-up route when `mock.signUpEnabled` is true or the OpenAPI sign-up operation exists.
- sign-out action.
- current session lookup or local session restore.
- private route guard.
- 401 cleanup and sign-in redirect.

## Source Selection

- If `swaggerUrl` is non-empty, `workflow/05-openapi.md` tries to extract sign-in, sign-up, current user, and sign-out operations.
- If an auth operation is found in OpenAPI, generate a production-shaped API function for that operation.
- If an auth operation is not found, generate the same feature boundary with mock fallback behavior.
- If `swaggerUrl` is empty or unavailable, skip OpenAPI reads and generate auth mock fallback.
- Do not add a separate auth mode. Auth generation is always part of the admin shell.

## FSD Boundaries

- Route pages live in `pages/sign-in` and `pages/sign-up`.
- User actions live in separate feature folders:
  - `features/sign-in`
  - `features/sign-up`
  - `features/sign-out`
- Session/current-user DTOs and schemas live in `entities/session/model`.
- Current-session read API and query hook live in `entities/session/apis` and `entities/session/hooks` when backed by API or MSW.
- Token and persisted auth helper code lives in `shared/lib` or `shared/store` according to `auth-token-storage.md`.
- Auth pages assemble UI and feature hooks; they do not call request wrappers directly.

## Forms

- Use React Hook Form and Zod.
- Form schemas follow `rules/form-zod.md`.
- Sign-in schema validates email and password.
- Sign-up schema validates email, password, password confirmation, and display name.
- Password confirmation uses `.refine` with the path set to the confirmation field.

## Mutations

- Sign-in and sign-up use mutation hooks following `rules/mutation.md`.
- Successful sign-in stores token/session first, then redirects to `routes.afterSignIn`.
- Successful sign-up redirects to sign-in unless the extracted API response clearly returns a usable token.
- Sign-out clears token/session first, then redirects to `routes.afterSignOut`.
- Auth success and failure feedback follows `rules/error-feedback.md`.

## Mock Fallback Behavior

- Seed users come from `input/auth.md` `mock.seedUsers`.
- If `mock.seedUsers` is missing, generate one synthetic admin user using the locale and privacy rules in `input/defaults/mock.md`.
- Mock sign-in accepts only matching email and password from the in-memory user list.
- Mock sign-up rejects duplicate email addresses and appends a new synthetic user in memory.
- Mock current-session returns the signed-in user when token/session exists.
- Mock sign-out clears token/session and does not require a server response.
- Mock auth data resets on browser refresh when `persistence: memory`.

## Security Boundary

- Mock passwords are development-only seed values.
- Never generate real personal information in seed users.
- Do not log passwords, tokens, or authorization headers.
- Do not put token values in URLs, query params, or route state.
