# Web Admin Page Agent Kit

React 기반 admin 웹앱을 생성하기 위한 에이전트 지침 묶음입니다. 최종 산출물은 단순 골격이 아니라, 사용자가 실행하고 이후 디테일을 수정할 수 있는 기본 구동 앱이어야 합니다.

이 폴더는 공개 저장소 초기화용 버전입니다. 프로젝트명, API URL, 인증 seed, 리소스 목록, 실행 리포트, 생성 캐시는 포함하지 않습니다.

## What It Builds

- Vite + React + TypeScript 기반 admin 앱
- FSD 계층: `app`, `pages`, `widgets`, `features`, `entities`, `shared`
- 대분류/소분류 sidebar navigation과 route map
- resource별 list page, table, pagination, search, filter
- enabled CRUD에 따른 detail/create/update/delete page, mutation, form
- Swagger/OpenAPI 미연동 시 auth/resource mock fallback
- mock rows가 실제 list table에 렌더링되는 runtime list smoke 검증

## Directory Map

```text
repo-root/
  agent.md                  # 실행 지침 입구
  00-04-*.md                # 프로젝트/package/TS/Vite/lint 기준
  input/                    # 프로젝트별 입력값
  workflow/                 # 00-09 실행 단계
  rules/                    # 생성 규칙과 품질 기준
  reports/                  # 실행 후 리포트 및 compact manifests
```

## Quick Start

1. 이 폴더의 내용을 새 프로젝트 루트로 사용하거나, 대상 프로젝트 루트에 복사합니다.
2. `input/README.md`를 읽고 `input/*` 값을 프로젝트에 맞게 채웁니다.
3. 최초 리소스 생성 전 `input/resource-manifest.md`에 메뉴 카테고리와 리소스 라벨을 작성합니다.
4. Codex에게 `agent.md를 읽고 input/index.md 기준으로 admin 앱을 생성해줘.`라고 요청합니다.
5. 의존성 설치가 필요하면 package manager와 설치 목록을 확인한 뒤 승인합니다.
6. 완료 전 lint/typecheck/build/runtime list smoke 결과를 확인합니다.

## Input Files

- `input/project.md`: 프로젝트명, 앱 타입, 기본/지원 언어
- `input/stack.md`: React/Vite/TypeScript/Tailwind 버전, table library, `uiKit`, optional tools
- `input/design.md`: 색상, 폰트, radius, density, style token
- `input/api.md`: API base URL env key, Swagger/OpenAPI URL
- `input/auth.md`: 인증 방식, token storage, 권한 모델, action 목록
- `input/resource-manifest.md`: 최초 리소스 생성용 메뉴 카테고리와 리소스 라벨
- `input/resources/*.md`: materialization 이후 resource source of truth

## Resource Flow

처음에는 `resource-manifest.md`가 리소스 seed 역할을 합니다. `workflow/03-materialize-resources.md` 이후에는 `input/resources/*.md`가 route, API, columns, filters, search, CRUD 설정의 기준입니다. `input/resource-index.json`은 파생 cache file입니다.

## Completion Expectation

- 앱이 실행 가능한 상태여야 합니다.
- Swagger/OpenAPI가 비어 있거나 불완전하면 mock fallback으로 auth와 resource 화면이 동작해야 합니다.
- mock rows가 1개 이상이면 대표 list table에 row/cell이 실제 렌더링되어야 합니다.
- sign-in, sign-up when enabled, sign-out, private-route guard가 기본적으로 동작해야 합니다.
