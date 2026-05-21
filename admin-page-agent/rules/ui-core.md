# UI Core Rule

`shared/ui/core`는 업무 화면에서 반복되는 복합 컴포넌트 위치다.

## Examples

- `Table`
- `Pagination`
- `PageHeader`
- `DefaultSearchPanel`
- `ImageUpload`
- `DatePicker`
- `AsyncBoundary`
- `GlobalAlert`
- `GlobalConfirm`

## Rules

- 여러 도메인에서 재사용될 때만 core로 승격한다.
- 도메인 이름, API 호출, query hook을 직접 포함하지 않는다.
- label과 메시지는 prop 또는 i18n key로 받는다.
- split input의 `uiKit`에 맞는 primitive를 조합한다.

core 컴포넌트는 기능이 많아도 책임이 하나여야 한다.

## Verified Core Artifact Baseline

`shared/ui/core` 컴포넌트는 에이전트가 생성할 수 있다. 단, 생성 직후 바로
baseline으로 간주하지 않는다. 검증을 통과한 core artifact만 다음 실행에서
재사용할 안정 자산으로 승격한다.

승격 조건:

- typecheck and build pass.
- 해당 core artifact를 사용하는 대표 화면 runtime list smoke가 통과한다.
- 브라우저 console error가 없다.
- 사용자 입력의 `uiKit`, `tableLibrary`, 관련 package major version이 기록된다.
- `reports/core-artifacts.json`에 compact manifest로 기록된다.

manifest 예시:

```json
{
  "schemaVersion": 1,
  "artifacts": [
    {
      "name": "Table",
      "file": "src/shared/ui/core/Table.tsx",
      "library": "ag-grid",
      "libraryMajorVersion": "33",
      "uiKit": "shadcn-compatible",
      "verifiedBy": "runtime-list-smoke",
      "verificationRoute": "/orders",
      "status": "verified"
    }
  ]
}
```

재생성 규칙:

- matching verified manifest는 artifact `file`, `status: "verified"`, current `uiKit`, current `tableLibrary`, and relevant package major versions가 현재 입력/설치 상태와 일치하는 `reports/core-artifacts.json` entry다.
- matching verified manifest가 있으면 core artifact를 재생성하거나 덮어쓰지 않는다.
- resource 생성은 기존 core artifact의 public props/API에 맞춘다.
- `uiKit`, `tableLibrary`, 관련 package major version이 바뀌면 verified 상태를 재검증한다.
- runtime list smoke가 실패하면 해당 core artifact를 baseline으로 취급하지 않는다.
- 사용자가 명시적으로 core 재생성을 요청한 경우에만 verified artifact를 수정한다.
