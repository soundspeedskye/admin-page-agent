# Private Route Guard Rule

private route는 loader에서 접근 가능 여부를 결정한다.

## Auth

- admin 앱은 기본적으로 private route guard를 생성한다.
- `bearer-token`이면 `tokenStorage` 기준으로 token을 확인한다.
- `session`이면 프로젝트 session 확인 API를 사용한다.
- `authType: none`은 사용자가 명시적으로 unauthenticated admin shell을 요청한 경우에만 redirect guard를 생략한다.
- 401 발생 시 인증 관련 storage를 정리한다.
- sign-in redirect 경로는 `input/auth.md`의 `routes.signIn`을 사용한다.

## Permission

- `permissionType: none`이면 권한 검사를 건너뛴다.
- `role`이면 role 목록으로 접근을 판정한다.
- `menu-action`이면 pathname과 action으로 접근을 판정한다.
- create/edit path는 필요한 action이 없으면 forbidden으로 보낸다.

## Hard Entry

- 직접 진입이면 token/session을 먼저 확인하고 메뉴 정보를 다시 적재한다.
- current-session API 또는 auth mock handler가 있으면 현재 사용자를 복구하거나 검증한다.
- 메뉴 매칭 실패나 조회 실패는 sign-in 또는 forbidden으로 보낸다.

loader는 화면 렌더링 전에 실패를 확정해야 한다.
