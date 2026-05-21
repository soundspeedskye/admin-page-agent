# List Page Generation Rule

리스트 페이지는 resource 명세에서 생성한다.

## Required UI

- `PageHeader`.
- optional action buttons.
- search panel if `search.fields` exists.
- filters if `filters` exists.
- table with columns.
- server pagination if `pagination: server`.
- loading, empty, error states.

## Data Flow

- URL query params drive page, pageSize, search, filters.
- query hook receives params DTO.
- table receives rows and total count.
- pagination updates URL page.
- filter changes reset page to 1.

## File Rule

- Page composes widgets and features.
- Entity owns DTO, API, query hook, column defs.
