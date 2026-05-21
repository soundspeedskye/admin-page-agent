# 03 Materialize Resources

리소스 manifest를 기준으로 누락된 리소스별 입력 파일만 생성한다.

## Purpose

- Create missing per-resource input files from the resource manifest.
- Preserve already materialized resource files as the source of truth.

## Read

- `input/index.md`
- existing `input/resources/*.md` files
- `input/resource-manifest.md` only for first materialization or explicitly requested missing-resource materialization
- `input/resource.template.md`
- `input/defaults/crud.md`

## Generate

- `input/resources/{resource}.md` only for manifest labels that do not already have a resource file.
- A diff proposal only when an existing resource file must change.
- `input/resource-index.json` after resource materialization or after confirming existing resource files.

## Resource Index

- Generate or refresh `input/resource-index.json` from `input/resources/*.md`.
- `resource-index.json` is a derived cache and must not become source of truth.
- Include only shallow fields needed for planning:
  - `resource`
  - `label`
  - `entityName`
  - `route`
  - `listApi`
  - `navigation.category`
  - `navigation.order`
  - `navigation.icon`
  - `crud`
  - `rowIdField`
  - `defaultPageSize`
- Do not include `columns`, `filters`, `search`, `crudApis`, or mock row data in the index.
- If the index is missing, stale, or inconsistent with `input/resources/*.md`, discard and regenerate it.
- Do not edit `resource-index.json` directly; update the relevant resource file and regenerate the index.

## Rules

- Do not overwrite existing resource files.
- Do not update existing resource files from the manifest directly.
- If an existing resource needs a label, category, route, API, CRUD, or column change, produce a minimal diff and apply it only after user approval.
- Manifest values are label and optional CRUD seeds for first materialization and missing-resource materialization.
- Use `resource.template.md` for the full resource file shape.
- If `resource`, `route`, or `listApi` cannot be inferred from an explicit project convention, ask the user before creating the resource file.
- Infer `entityName` from the confirmed resource id in PascalCase.
- Copy the manifest category and derived category/resource order into each new resource file under `navigation`.
- Normalize manifest `crud` into the generated resource file's explicit `crud` object.
- After this workflow, `input/resources/*.md` is the source of truth for resource, navigation, API, CRUD, columns, filters, and search.
- After this workflow, later workflows may use `input/resource-index.json` for shallow planning, but must read the specific resource file before generating files that depend on columns, filters, search, pagination, or CRUD API details.
- Later workflows must not read `input/resource-manifest.md`.
- Apply `input/defaults/crud.md` when manifest `crud` or individual CRUD keys are missing.
- Keep generated files resource-scoped.

## Validation

- Manifest entries contain `label` and optional `crud.create`, `crud.detail`, `crud.update`, and `crud.delete` boolean values only.
- Materialized resource `resource` is kebab-case.
- Materialized resource `route` starts with `/`.
- Materialized resource `listApi` includes method and path.
- Materialized resource has `resource`, `label`, `entityName`, `route`, `listApi`, `navigation`, `crud`, `crudApis`, `pagination`, and `columns`.
- Existing resource files are skipped unless a user-approved diff is applied.
