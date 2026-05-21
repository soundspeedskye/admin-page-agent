# Sidebar Navigation Rule

Sidebar is generated from materialized `input/resources/*.md`.

## Parent

- Has `label` from `navigation.category`.
- Has optional `icon`.
- Has `children`.
- Controls grouping and order.

## Child

- Has `label`.
- Has `resource`.
- Has `path`.
- Has optional `api`.
- Navigates to a list page by default.

## Rules

- Active state is based on pathname.
- Parent opens when a child route is active.
- Parent order uses the lowest child `navigation.order` in the category; child order uses each resource file's `navigation.order`.
- Icons use `Icons` registry or lucide.
- Missing icon falls back to a neutral icon.
- Menu labels use i18n keys when i18n is enabled.
- Do not read `input/resource-manifest.md` after materialization.
