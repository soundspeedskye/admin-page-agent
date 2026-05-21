# Filter Query Param Rule

목록 필터는 URL query string과 동기화한다.

## Hooks

- 기존 공통 query param hook이 있으면 재사용한다.
- 없으면 `useListQueryParams`처럼 목록 전용 hook을 만든다.

## Rules

- 필터 변경 시 page는 1로 초기화한다.
- page와 pageSize도 URL에 반영한다.
- 값이 비어 있으면 query param을 삭제한다.
- 뒤로가기 대응을 위해 POP navigation에서 URL 값을 재해석한다.
- 날짜 request 값은 start/end 규칙에 맞춰 UTC ISO로 변환한다.

## Search Panel

- keyword type과 keyword는 로컬 입력 상태를 둔다.
- Enter와 search icon이 같은 submit 함수를 호출한다.
