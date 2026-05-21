# Query Key Rule

query key는 hook 옆 또는 API query options 옆에 factory로 둔다.

## Pattern

```ts
export const getUserListQueryKeys = (params?: UserListParamsDto) =>
  params ? ['userList', params] : ['userList'];
```

## Rules

- 목록 key는 domain list 이름을 첫 원소로 둔다.
- 상세 key는 id 또는 params를 포함한다.
- params가 없을 때 invalidate 가능한 base key를 반환한다.
- 문자열 key를 여러 파일에 직접 반복하지 않는다.
- invalidate/removeQueries는 factory 결과를 사용한다.

## Avoid

- `['list']`처럼 도메인이 없는 key.
- 같은 데이터에 서로 다른 key 이름 사용.
- 객체 params를 일부만 key에 넣는 패턴.
