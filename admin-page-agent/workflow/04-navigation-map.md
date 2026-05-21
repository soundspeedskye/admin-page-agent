# 04 Navigation Map

대분류와 소분류 메뉴를 route와 sidebar 구조로 변환한다.

## Read

- `input/resource-index.json` first.
- `input/resources/{resource}.md` only for resources missing from the index or when validating an inconsistent index.

## Generate Or Update

- `app/routing/paths.ts`
- navigation menu model or constants consumed by the admin shell.
- menu icon keys or registry input.

## Rules

- Parent category is navigation only.
- Parent categories come from each indexed resource's `navigation.category`.
- Parent order follows the lowest indexed `navigation.order` in each category; child order follows each indexed resource's `navigation.order`.
- Child category links to one indexed materialized resource.
- Path constants use uppercase snake case.
- Route path comes from `input/resource-index.json` `route`.
- If `input/resource-index.json` is missing, stale, or inconsistent with `input/resources/*.md`, stop route generation and return to `03-materialize-resources.md` to regenerate it.
- Missing resource files or routes must be reported before generation.
- Do not create or edit layout components in this workflow.
- Route tree updates happen when concrete pages are generated.
- Do not read `input/resource-manifest.md` in this workflow.

Use `sidebar-navigation.md` and `route-map.md`.
