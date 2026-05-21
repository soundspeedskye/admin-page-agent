# 05 OpenAPI

Swagger/OpenAPI가 있으면 DTO와 API 후보를 먼저 추출한다.

This workflow reads OpenAPI only when `input/api.md` has a non-empty `swaggerUrl`.
If `swaggerUrl` is empty, skip OpenAPI fetch/read entirely and use mock fallback from resource files and auth input.

## Read

- non-empty `swaggerUrl` from `input/api.md`.
- `input/auth.md` for required auth routes, token policy, and fallback seed users.
- `input/resource-index.json` for resource list, `listApi`, route, and enabled CRUD flags.
- `input/resources/{resource}.md` only when an enabled CRUD action needs explicit `crudApis.*`, or when fallback generation needs columns, filters, or search details.

## Extract

- Do not reason over the full OpenAPI document.
- For each resource, always extract the operation matching `listApi`.
- For each enabled CRUD key, extract only the matching CRUD operation.
- Extract auth operation candidates for sign-in, sign-up, current-session, and sign-out.
- Use explicit `crudApis.*` first. If empty, infer REST-style candidates from `listApi` and match them in OpenAPI.
- If an enabled CRUD operation cannot be matched, use operation-level mock fallback for that action instead of reading unrelated OpenAPI paths.
- If an auth operation cannot be matched, use auth mock fallback for that operation instead of reading unrelated OpenAPI paths.
- Extract only schemas reachable from the selected operations through request bodies, responses, parameters, and recursive `$ref` references.
- request and response DTOs for selected operations.
- enum values.
- nullable and required fields.
- path method, params, query, body.

## Produce Extraction Result

- selected list and CRUD operations.
- request/response DTO shapes.
- query, path, and body parameter shapes.
- enum, nullable, and required field metadata.
- operation-level fallback markers when an operation cannot be extracted.
- auth fallback markers for unmatched sign-in, sign-up, current-session, or sign-out operations.

## Rule

Swagger로 알 수 없는 label, order, and route planning values are read from `input/resource-index.json`.
Swagger로 알 수 없는 search, filter, columns, pagination, and `crudApis.*` details are read only from the selected `input/resources/{resource}.md` file.
`input/resource-manifest.md` is not read in this workflow.

## Fallback

If Swagger/OpenAPI is unavailable, do not stop generation.

Use `mock-data-fallback.md` and `auth-generation.md` to define fallback shapes and mock artifacts for later generation.

Fallback applies when `swaggerUrl` is empty, fetch fails, the fetched document is not valid OpenAPI, or a selected resource/auth operation cannot be extracted.

Resource operation-level mock fallback must be provided through MSW handlers only. App API modules must keep calling the typed request wrapper and must not import mock data or `mock-db.ts`.

If a real API base URL is configured but only some selected resource operations fall back to mock, report the mixed-source operations and require MSW to be enabled before generation continues.
If only auth operations fall back, follow `auth-generation.md` and use MSW handlers when available or the client-side auth fallback adapter when MSW is disabled.

Use `resource-from-swagger.md`, `auth-generation.md`, and `auth-token-storage.md`.
