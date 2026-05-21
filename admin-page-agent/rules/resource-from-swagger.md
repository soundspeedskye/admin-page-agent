# Resource From Swagger Rule

Swagger/OpenAPI는 DTO와 API 초안을 만드는 원천이다.

## Read

- `openapi`, `info`, and only the selected `paths`.
- matching operation for each resource `listApi`.
- matching operations for enabled CRUD actions only.
- reachable schemas from selected operations only.

If the full OpenAPI document must be fetched first, reduce it to the selected operation subset before using it as generation context.

## Produce Extraction Result

- TypeScript DTO interface shape.
- Zod response schema shape when useful.
- API operation metadata for the typed `request` wrapper.
- query params DTO shape from endpoint query parameters.
- enum unions from schema enum.

## Operation Selection

- `listApi` is always selected.
- `crudApis.create` is selected only when `crud.create` is true.
- `crudApis.detail` is selected only when `crud.detail` is true.
- `crudApis.update` is selected only when `crud.update` is true.
- `crudApis.delete` is selected only when `crud.delete` is true.
- Empty `crudApis.*` values may be inferred from `listApi` using REST conventions, then matched against OpenAPI.
- Unmatched selected operations must use operation-level mock fallback or stop for user input.

## Merge With Input

- Swagger decides technical shape.
- `input/resources/*.md` decides label, order, visible columns, filters after materialization.
- If names conflict, report the conflict before generating.

Swagger alone must not decide UI labels.
