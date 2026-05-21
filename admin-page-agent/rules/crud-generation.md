# CRUD Generation Rule

Generate CRUD only when enabled by manifest or resource input.

## Read

- `input/defaults/crud.md`, `input/resource-manifest.md` during materialization, `input/resources/{resource}.md` after materialization
- OpenAPI extraction result or mock fallback extraction result

## Resource Config

`crud` keys are `create`, `detail`, `update`, and `delete`.

`input/resource-manifest.md` may provide initial CRUD decisions per resource seed. During materialization, normalize those values into the generated `input/resources/{resource}.md` file.

## Defaults And Validation

- Missing CRUD keys inherit from `input/defaults/crud.md`; without a default file, all actions default to `false`.
- `crud`, when present, must be an object containing only boolean `create`, `detail`, `update`, and `delete` keys.
- Non-boolean CRUD values stop generation for that resource.
- `crudApis`, when present, must be an object containing only `create`, `detail`, `update`, and `delete` method/path values.
- Empty `crudApis.*` values mean "infer from `listApi` when the matching CRUD flag is true."
- If a CRUD flag is true, code generation must use an extracted OpenAPI operation or mock fallback operation for that action.

## Generate When Enabled

- `detail`: detail API, detail query hook, detail page route.
- `create`: create API mutation, create form schema, create page route.
- `update`: update API mutation, edit form schema, edit page route.
- `delete`: delete API mutation, confirm flow from list/detail page.

## API Source

- Use extracted OpenAPI operations for enabled CRUD actions.
- Use `crudApis.*` from the resource file when present.
- If `crudApis.*` is empty, infer the operation from `listApi` using REST conventions before falling back to mock generation.
- Do not generate CRUD from `listApi` alone.

## Data Flow

- Read/list/detail APIs and query hooks live in `entities/{resource}`.
- Create/update/delete APIs and mutation hooks follow `mutation.md`.
- Create/update form schemas follow `form-zod.md` and live in the matching feature action folder.
- Page components live in `pages/{resource}`.
- List actions are visible only for enabled actions.
- Successful mutations follow `cache-invalidation.md`.
- Mock fallback follows `mock-data-fallback.md`.

## Mock Fallback

When CRUD is enabled with mock fallback, use `mock-data-fallback.md`.
