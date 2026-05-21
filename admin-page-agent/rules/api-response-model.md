# API Response Model Rule

API 응답 타입은 Swagger/OpenAPI에서 먼저 추론한다.

## Inference Order

1. matched path response schema.
2. referenced `components.schemas`.
3. existing request wrapper types.
4. fallback mock response shape: `{ rows: T[]; count: number }`.
5. 알 수 없으면 사용자에게 응답 shape를 확인한다.

## Common Examples

- object wrapper: `{ row: T }`.
- list wrapper: `{ rows: T[], count: number }`.
- data wrapper: `{ data: T[] }`.
- direct array: `T[]`.

## Params

- `ListParams`: page, pageSize, sortBy, sortDirection.
- `PaginationParams`: page, pageSize.
- `SortParams`: sortDirection.

## Rule

- 서버 DTO는 `entities/{domain}/model/*.dto.ts`에 둔다.
- schema 검증용 타입은 `*.schema.ts`에 둔다.
- response wrapper는 API 함수 generic으로 명시한다.
- 특정 wrapper 형태를 강제로 적용하지 않는다.
