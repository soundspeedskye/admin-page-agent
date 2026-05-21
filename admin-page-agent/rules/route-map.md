# Route Map Rule

라우트는 `app/routing` 아래에서 관리한다.

## Files

- `paths.ts`: 모든 path 상수.
- `router.tsx`: React Router route tree.

## Path Rule

- path 값은 문자열 literal로 한 곳에만 둔다.
- 동적 segment는 `:id`, `:userId`처럼 명확하게 쓴다.
- 목록, 상세, 생성, 수정 경로를 같은 도메인 prefix 아래 둔다.

## Router Rule

- 공개 인증 페이지는 최상위 route로 둔다.
- 인증 필요한 페이지는 `PrivateLayout` children으로 둔다.
- private loader에서 인증, 권한, 메뉴 접근을 검사한다.
- not found는 `path: '*'`로 처리한다.

Path planning workflows may prepare `paths.ts` before page files exist. When a concrete page route is generated, update `paths.ts` and `router.tsx` together.
