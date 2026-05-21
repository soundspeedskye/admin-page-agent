# Error Feedback Rule

사용자 피드백은 toast, global alert, route redirect로 나눈다.

## Toast

- 일반 성공은 project toast adapter를 사용한다.
- 일반 실패도 같은 toast adapter를 사용한다.
- 서버 error message가 있으면 그 값을 표시한다.

## Global Alert

- 삭제, 이탈, 위험 작업, 확인이 필요한 생성/수정에 사용한다.
- project global alert/confirm adapter로 호출한다.
- action 안에 최종 mutation을 둔다.

## Redirect

- 401: token 정리 후 sign-in.
- 403: forbidden.
- 500: server-error.

에러를 조용히 삼키지 않는다.
