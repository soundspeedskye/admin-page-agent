# Resource Template

이 파일은 `input/resources/{resource}.md`의 기준 형식이다.
Mock fallback이 활성화되어 있고 Swagger/OpenAPI가 없으면 `mock.rows`까지 materialize한다.

<!-- prettier-ignore-start -->
```yaml
resource: <resource-id>
label: <RESOURCE_LABEL>
entityName: <PascalCaseEntity>
route: <LIST_ROUTE_PATH>
listApi: GET <LIST_API_PATH>

navigation:
  category: <CATEGORY_LABEL>
  order: 10
  icon: <LUCIDE_ICON_NAME>

crud:
  create: false
  detail: false
  update: false
  delete: false

crudApis:
  create:
  detail:
  update:
  delete:

pagination: server
defaultPageSize: 20
defaultSort:
rowIdField: id

search:
  fields:
    - <searchableField>

filters:
  - key: <filterField>
    label: <FILTER_LABEL>
    type: enum
    options:
      - <OPTION>

columns:
  - key: id
    label: ID
    type: number
    flags: searchable=false, filterable=false, sortable=true

mock:
  enabledWhenSwaggerUnavailable: true
  rowCount: 10
  dataFile: src/shared/api/mocks/data/<resource-id>.mock.ts
  visualSampleReport: reports/mock-data-sample-report.md
  rows:
    - id: 1
      <fieldKey>: <sampleValue>
```
<!-- prettier-ignore-end -->
