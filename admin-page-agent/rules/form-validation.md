# Form Validation Rule

검증은 클라이언트 schema, 서버 중복 체크, 제출 전 확인으로 나눈다.

## Client

- 필수값은 zod `min`, `enum`, `refine`으로 처리한다.
- 날짜 범위는 시작/종료 비교를 refine에 둔다.
- URL 등 형식 검사는 regex나 전용 parser를 사용한다.

## Server

- 중복 체크 mutation은 실제 생성 mutation 전에 실행한다.
- 중복 결과가 field 목록이면 `form.setError`로 매핑한다.
- 서버의 일반 실패는 toast로 표시한다.

## Confirm

- 위험하거나 공개 영향이 있는 생성/수정은 global alert로 확인한다.
- 확인 action 안에서 최종 mutation을 실행한다.

검증 로직을 UI JSX 안에 길게 섞지 않는다.
