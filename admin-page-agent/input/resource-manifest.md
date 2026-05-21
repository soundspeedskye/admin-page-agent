# Resource Manifest

This file lists resource categories, menu labels, and optional CRUD decisions.

## Customize Before Running

- Add the real menu categories and resource labels for your project before running `agent.md`.
- Remove any category or label that should not be generated.
- Each `###` heading becomes `navigation.category` in the generated resource file.
- Each `- label:` item becomes one resource seed.
- Add `crud` when the resource should generate create/detail/update/delete behavior.
- Keep route, API, columns, filters, and search fields in `input/resources/*.md` after materialization.

## Rule

- Use this file only to identify desired resource categories, menu labels, and initial CRUD decisions before first materialization.
- Do not put route, API, column, filter, or search fields here.
- Technical fields such as `resource`, `entityName`, `route`, `listApi`, and `columns` belong in `input/resources/*.md`.
- `crud`, when present, must contain only boolean `create`, `detail`, `update`, and `delete` keys.
- Missing `crud` keys inherit from `input/defaults/crud.md`.
- Use `resource.template.md` for the full resource file shape.
- Do not overwrite existing files in `input/resources`.
- After materialization, use `input/resources/*.md` as the source of truth and do not read this manifest in later workflows.

## Resources

Add project resources here before the first run.
