# Zustand Store Rule

전역 UI 상태와 앱 설정은 `shared/store`에 둔다.

## Examples

- global alert
- global confirm
- selected header
- language
- auth token helper state
- hard entry navigation state

## Pattern

- state interface와 action interface를 분리한다.
- `initialState`를 명시한다.
- `open`, `close`, `toggle` 같은 명령형 action을 제공한다.
- 외부에서 바로 호출할 helper가 필요하면 별도 export한다.

## Avoid

- 서버 캐시를 zustand에 중복 저장하지 않는다.
- 도메인 상세 데이터를 전역 store에 오래 보관하지 않는다.
