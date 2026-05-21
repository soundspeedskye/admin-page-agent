# Mock Data Fallback Rule

Swagger/OpenAPI를 사용할 수 없을 때 resource와 auth fallback을 생성한다.
Resource fallback은 resource 명세에서 DTO, schema, API, visual sample mock data를 생성한다.
Auth fallback은 `input/auth.md`에서 seed user와 route 정책을 읽어 로그인/회원가입이 클라이언트에서 동작하게 만든다.

## Trigger

- `swaggerUrl`이 비어 있거나 fetch/validation이 실패한다.
- 선택된 resource operation을 OpenAPI에서 찾을 수 없다.
- 선택된 auth operation을 OpenAPI에서 찾을 수 없다.
- When `swaggerUrl` is empty, do not fetch/read OpenAPI before fallback generation.

## Read

- `input/api.md`
- `input/auth.md`
- `input/stack.md`
- `input/defaults/mock.md`
- `input/resources/{resource}.md`

## Generate

- DTO interfaces from resource columns, filters, search fields, and enabled CRUD actions.
- Zod schemas for generated DTOs and list params.
- production-shaped API modules for `listApi` and enabled CRUD paths.
- visual sample rows at `shared/api/mocks/data/{resource}.mock.ts`.
- synthetic auth seed users from `input/auth.md` `mock.seedUsers`.
- `shared/api/mocks/mock-registry.ts` and memory-only `mock-db.ts`.
- MSW handlers only when `optionalTools.msw` is true.

## Response Shape

Resource list fallback:

```ts
{ rows: TRow[]; count: number; }
```

Auth fallback:

```ts
{
  accessToken: string;
  user: {
    id: string;
    email: string;
    name: string;
    role: string;
  };
}
```

## Visual Sample Data Rules

- Purpose: help users visually understand generated admin list/detail/form UI.
- Follow `input/defaults/mock.md` for `rowCount`, `locale`, `dataRealism`, and `privacy`.
- Generate realistic but fully synthetic rows from resource label, columns, filters, search fields, enum options, and CRUD context.
- For Korean admin apps, prefer `ko-KR` names, identifiers, dates, contact-like values, and currency-like amounts.
- Never use real personal information. Emails must use safe example domains.
- Do not use generic `${label} 샘플 ${index}` text unless no semantic hint exists.
- Preserve DTO types exactly and use declared enum option values exactly.
- Include at least one row per enum option when `rowCount` allows.
- Keep related fields coherent, such as status/date/amount combinations.
- Distribute date/datetime values across recent, pending, and past cases.
- Use stable deterministic unique IDs.

## Field Hints

- `patientName`, `customerName`, `userName`: synthetic Korean person names.
- `providerName`, `doctorName`, `staffName`: synthetic staff names with role context.
- `appointmentNo`, `claimNo`, `paymentNo`: structured identifiers like `APT-20260515-001`.
- `phone`, `email`, `address`: safe synthetic contact values.
- `amount`, `price`, `balance`: realistic numbers for the field meaning.
- unknown text: infer from key/label first; use `-` only as the final fallback.

## MSW Boundary

- App API modules must call the typed `request` wrapper and must not import mock infrastructure.
- MSW handlers are the runtime mock boundary and may import `mock-db.ts`.
- `mock-db.ts` seeds from `data/{resource}.mock.ts`, mutates in memory, and resets on refresh.
- Handler output must use `{ rows: TRow[]; count: number; }`.
- Generate list handlers first and CRUD handlers only for enabled CRUD actions.
- Auth handlers may import the auth seed users and mutate the in-memory auth user list.
- Auth handlers must support sign-in, sign-up when enabled, current-session lookup, and sign-out.
- If MSW is disabled, generate client-side auth fallback through the auth feature adapter while keeping resource fallback rules unchanged.

## Auth Fallback Rules

- Seed users must be synthetic and safe for development.
- If a fallback seed user is required, use a reserved example domain and mark it as mock-only.
- Sign-in fails when email or password does not match.
- Sign-up fails when the email already exists.
- New sign-up users are stored in memory and reset on refresh when `persistence: memory`.
- Generated access tokens are deterministic enough for UI testing but must not be presented as secure production tokens.

## Report

- Report which Swagger/OpenAPI URL failed or was empty.
- Report which resources and auth operations used mock fallback.
- Report which mock sample strategy was generated.
- Report whether MSW handlers were generated.
