# FSD Layer Rule

계층은 위에서 아래로만 조립한다.

## Layers

- `app`: 전역 설정과 provider.
- `pages`: route 단위 조립.
- `widgets`: 여러 도메인을 묶은 업무 블록.
- `features`: 사용자 행위, CUD, 인증 흐름.
- `entities`: 도메인 모델, 조회 API, query, table.
- `shared`: 도메인 독립 공용 코드.

## Import Direction

- `pages`는 `widgets/features/entities/shared`를 조립할 수 있다.
- `widgets`는 `features/entities/shared`를 사용할 수 있다.
- `features`는 `entities/shared`를 사용할 수 있다.
- `entities`는 `shared`만 사용할 수 있다.
- `shared`는 다른 계층을 import하지 않는다.

## Mock Infrastructure Exception

- Generated files under `shared/api/mocks/**` are dev/test API infrastructure.
- `shared/api/mocks/**` may contain resource-id based mock fixture files and handler names.
- `shared/api/mocks/**` must not be imported by `entities`, `features`, `widgets`, or `pages`.
- `shared/api/mocks/**` must not import `entities`, `features`, `widgets`, or `pages`; use shared types only.

## 금지

- `entities`에서 `features` import 금지.
- `shared`에 비즈니스 도메인 이름 넣기 금지.
- `pages`에 API 호출 구현을 직접 넣지 않는다.
