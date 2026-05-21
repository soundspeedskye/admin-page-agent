# Project Structure

이 프로젝트는 FSD 기반 계층형 구조를 사용한다.

```txt
src/
  app/       전역 provider, routing, style, app-level ui
  pages/     URL 라우트 단위 화면 조립
  widgets/   여러 entity/feature를 조합한 화면 블록
  features/  create/update/delete/sign-in 등 사용자 행위
  entities/  도메인 데이터, read api, query, model, table
  shared/    공용 ui, api wrapper, hooks, store, lib, assets
  test/      전역 테스트 setup
```

## 계층 책임

- `app`: 앱 부팅, 라우터, QueryClient, 전역 스타일, layout.
- `pages`: 라우트 진입점이며 데이터/feature/widget를 조립한다.
- `widgets`: 페이지 안의 큰 업무 블록이다.
- `features`: 사용자의 행위나 CUD 로직을 담는다.
- `entities`: 서버 도메인과 조회 중심 모델을 담는다.
- `shared`: 도메인 독립적인 공용 코드만 담는다. Mock infrastructure 예외는 `rules/fsd-layer.md`를 따른다.

## 도메인 내부

```txt
domain/
  apis/
  hooks/
  model/
  ui/
  lib/
  index.ts
```

Bootstrap 단계는 top-level FSD와 shared infrastructure 폴더를 만들 수 있다. Domain/action 내부 폴더는 필요한 파일이 생길 때만 만든다.
