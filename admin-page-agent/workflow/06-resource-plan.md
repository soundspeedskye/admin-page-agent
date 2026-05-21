# 06 Resource Plan

각 resource별 생성 파일 목록을 확정한다.

## Read

- `input/resource-index.json` in split input mode.
- `input/resources/{resource}.md` only for resources selected for concrete generation, and only when columns, filters, search, pagination, or `crudApis.*` details are needed.
- `input/defaults/crud.md`.
- OpenAPI extraction result.
- mock fallback extraction result when Swagger/OpenAPI is unavailable.
- Do not read `input/resource-manifest.md`.

## Plan Per Resource

- entity folder.
- list API function.
- list query key.
- list query hook.
- column defs.
- list page.
- optional widget card.
- route registration.
- enabled CRUD actions.
- detail route and API when `crud.detail` is true.
- create route and mutation when `crud.create` is true.
- update route and mutation when `crud.update` is true.
- delete mutation and confirmation flow when `crud.delete` is true.

## Validate

- resource id is kebab-case.
- route is unique.
- list API exists.
- `resource-index.json` exists and matches the selected resource ids and routes.
- enabled CRUD operations have an extracted OpenAPI operation or mock fallback operation.
- columns are not empty.
- pagination/search/filter settings are explicit.

Use `domain-slice.md`, `query-key.md`, `query-hook.md`.
