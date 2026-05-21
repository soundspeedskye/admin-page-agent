# Agent Kit Input Guide

Read this file before running `agent.md`.

This folder contains project-specific input values for generating a runnable admin web app. Fill the empty values with real project values before running the agent.

## Files To Customize

Edit these files first:

- `project.md`: project name, type, default language, supported languages.
- `stack.md`: React/Vite/TypeScript/Tailwind versions, table library, UI kit, optional tools.
- `design.md`: colors, font, radius, density, UI kit theme, style token notes.
- `api.md`: API base URL env key and optional Swagger/OpenAPI URL.
- `auth.md`: auth type, token storage, auth routes, mock seed users, permission model, available actions.
- `resource-manifest.md`: first menu categories, resource labels, and initial CRUD decisions.

Leave `api.md` `swaggerUrl` empty when the real API is not ready. The agent should skip OpenAPI reading and use mock fallback rules so generated auth and resource screens are usable without a backend.

In `resource-manifest.md`, add the real project menu categories and labels. Each `###` heading becomes `navigation.category`, and each `- label:` item becomes one resource seed. Add `crud.create`, `crud.detail`, `crud.update`, and `crud.delete` booleans when the resource should generate more than a list page. Do not put technical fields such as `resource`, `route`, `listApi`, or `columns` there.

Before a full run, make sure at least one resource seed exists. The runtime list smoke expects mock rows to render in a generated list table when Swagger/OpenAPI is unavailable.

## Files Usually Not Edited First

- `index.md`: agent-facing entrypoint listing input file locations and reading rules.
- `resource.template.md`: template for generated `input/resources/{resource}.md` files.
- `defaults/crud.md`: default CRUD behavior when a resource omits CRUD keys.
- `defaults/mock.md`: default mock fallback behavior when API/OpenAPI is unavailable.

## After Resource Materialization

Once `input/resources/*.md` files exist, they become the source of truth for:

- resource id, label, route, and list API
- navigation category and order
- CRUD settings
- columns, search, and filters

Do not use `resource-manifest.md` for later route, API, column, or CRUD changes unless explicitly generating missing resources.
