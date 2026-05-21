# Table AG Grid Rule Optional

split input의 `tableLibrary: ag-grid`일 때 이 규칙을 적용한다.

대량 목록은 AG Grid 기반 `shared/ui/core/Table.tsx` wrapper를 사용한다.
AG Grid wrapper의 생성, 검증 후 승격, 재사용은 `ui-core.md`의
`Verified Core Artifact Baseline`을 따른다.

## Rules

- row id는 resource `rowIdField`를 우선한다.
- 없으면 Swagger schema의 id 필드를 추론한다.
- 그래도 없으면 `id`, `_id` 순서로 fallback한다.
- 서버 정렬을 기준으로 하고 client sort는 기본 비활성화한다.
- sortable column은 custom header에서 asc, desc, none을 순환한다.
- checkbox가 필요하면 `hasCheckbox`와 `isRowSelectable`을 사용한다.
- 빈 데이터는 AG Grid의 no-rows overlay(`noRowsOverlayComponent` 또는 `overlayNoRowsTemplate`)로 표시한다.
- pagination은 wrapper의 `paginationInfo`를 사용한다.

## Column Defs

- 도메인 column 정의는 `entities/{domain}/lib/*column-defs.tsx`에 둔다.
- cell renderer는 표시 로직만 포함한다.
- row action은 callback prop으로 넘긴다.
