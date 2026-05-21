# 01 Intake

프로젝트 입력값을 먼저 확보한다.

## Input Entry

- Prefer `input/index.md`.
- If `input/index.md` is missing, create or request the split input file set.
- Validate only files needed for the current workflow.
- Do not require all resource files before `03-materialize-resources.md` runs.
- Intake must not block only because `input/resources/*.md` files do not exist yet.

## Steps

1. `input/index.md`가 있는지 확인한다.
2. 없으면 split input 파일 세트를 만들거나 사용자에게 요청한다.
3. 현재 workflow에 필요한 input 파일만 읽는다.
4. `input-validation.md` 기준으로 필수값을 검증한다.
5. 비어 있는 필수값을 체크리스트로 정리하고 생성 전 사용자에게 요청한다.
6. `swaggerUrl`이 있으면 접근 가능 여부만 확인한다.
7. `swaggerUrl`이 비어 있으면 OpenAPI 확인을 건너뛰고 resource/auth mock fallback 흐름으로 진행한다.

## Required Before Materialization

- project name
- primary color
- API base env
- auth type, token storage, auth routes, permission type, and actions
- resource manifest labels and optional CRUD decisions when `input/resources/*.md` is empty

## Required During Resource Materialization

- manifest resource labels and optional CRUD decisions only for first materialization or explicitly requested missing-resource materialization
- `resource.template.md`
- resource id, route, and list API values when they cannot be inferred from explicit project convention

## Required After Materialization

- `input/resources/*.md`
- resource `navigation`, `route`, `listApi`, CRUD, columns, filters, and search values from resource files
- do not use `input/resource-manifest.md` as source of truth

입력값은 workflow나 rules에 직접 쓰지 않는다.
현재 workflow에 필요한 필수값이 비어 있으면 코드 생성을 시작하지 않는다.
Auth는 admin 기본 골격이므로 `swaggerUrl`이 비어 있어도 auth API endpoint 값을 요구하지 않는다.
