# 08 Generate List Pages

resource 명세로 기본 리스트 페이지를 생성한다.

## Read

- `input/resource-index.json` for generation scope, route, label, entityName, listApi, navigation, CRUD flags, rowIdField, and defaultPageSize.
- `input/resources/{resource}.md` only for the selected resource being generated, because columns, filters, search, pagination, and `crudApis.*` are detailed resource data.
- OpenAPI extraction result for selected operations.
- mock fallback extraction result for selected fallback operations.
- Do not read `input/resource-manifest.md`.

## Generate Per Resource

- `pages/{resource}/{Resource}List.tsx`
- `entities/{resource}/apis/get-{resource}-list.ts`
- `entities/{resource}/hooks/use-{resource}-list-query.ts`
- `entities/{resource}/model/{resource}.dto.ts`
- `entities/{resource}/model/{resource}.schema.ts`
- fallback mock artifacts from `mock-data-fallback.md` when mock fallback is active
- `entities/{resource}/lib/{resource}-column-defs.tsx`
- optional `widgets/{resource}-management/ui/*TableCard.tsx`
- route tree entries for generated pages.

When mock fallback is active, generated mock row files are part of the visual review surface of the admin UI. They must follow `rules/mock-data-fallback.md` Visual Sample Data Rules instead of generic placeholder text.

## Core Artifact Reuse

- Follow `rules/ui-core.md` `Verified Core Artifact Baseline` before creating or modifying `shared/ui/core` wrappers.
- Resource generation must use matching verified `shared/ui/core` artifacts when available.
- Do not read or rewrite verified core artifact source unless a compile error or smoke failure points to it.
- Adapt generated resource pages, widgets, and column defs to the existing core artifact public props/API.
- If no matching verified artifact exists, generate the required core artifact once and leave promotion to `09-review-and-verify.md`.

## Optional CRUD

Use `crud-generation.md`.

Generate CRUD pages, mutations, form schemas, and list row actions only for enabled CRUD keys.

## Token Budget Rule

- Do not read every file in `input/resources/*.md` during list page generation.
- Iterate from `input/resource-index.json`, then read one `input/resources/{resource}.md` at a time for the resource currently being generated.
- If the user requests a single resource update, read only `resource-index.json` and that resource file.
- If `resource-index.json` is missing or stale, stop and return to `03-materialize-resources.md` to regenerate it before continuing.
- Prefer the compact core artifact manifest over rereading verified `shared/ui/core` source files during resource-only generation.

## Include

- page header.
- search panel.
- filters.
- table.
- server pagination.
- loading state.
- empty state.
- error feedback.

Use `project-consistency.md`, `list-page-generation.md`, `table-column-generation.md`, and `ui-core.md`.
