# Auth Token Storage Rule

`authType`과 `tokenStorage`는 `input/auth.md`에서 읽는다.

## Supported Auth Types

- `bearer-token`: store a bearer token and attach it to HTTP requests.
- `session`: use the project session/current-user API when available.

admin generation expects auth to exist. Do not skip private route guards unless the user explicitly changes the auth input and accepts an unauthenticated admin shell.

## Supported Storage

- `memory`: keep token and current user in memory only.
- `sessionStorage`: persist token and current user for the browser tab session.
- `localStorage`: persist token and current user across browser restarts.

## Token Helpers

- Provide one helper module for read, write, and clear operations.
- Do not duplicate token state in multiple stores.
- Keep token helper APIs small:
  - `getAccessToken`
  - `setAccessToken`
  - `clearAccessToken`
  - `getCurrentUser`
  - `setCurrentUser`
  - `clearCurrentUser`
- If using Zustand, follow `rules/zustand-store.md` and keep server cache out of the store.

## Request Integration

- `bearer-token` requests attach `Authorization: Bearer <token>` in the typed request wrapper.
- Auth API functions still call the same typed request wrapper as resource APIs.
- API modules must not read from mock data directly.
- MSW handlers, when generated, are the mock boundary.

## Cleanup

- On 401, clear token and current user before redirecting to `routes.afterSignOut` or `routes.signIn`.
- On explicit sign-out, clear token and current user before navigation.
- On failed sign-in or sign-up, do not leave partial token or user state.

## Hard Entry

- When a user opens a private URL directly, the private route loader checks token/session before rendering.
- If token/session is missing, redirect to `routes.signIn`.
- If token exists and a current-session API or MSW handler exists, validate or restore the current user before rendering.
- If validation fails, clear auth storage and redirect to sign-in.
