# Cache Invalidation Rule

mutation 성공 후 데이터 동기화는 query key factory를 사용한다.

## Rules

- 생성 성공: 목록 key를 invalidate한다.
- 수정 성공: 목록 key와 상세 key를 invalidate한다.
- 삭제 성공: 목록 key invalidate 또는 removeQueries를 사용한다.
- 상세 삭제 후에는 상세 key를 removeQueries한다.
- 여러 도메인이 영향받으면 영향을 받는 key를 모두 명시한다.
- 화면 이동은 page/widget의 mutation `onSuccess`에서 처리한다.

## Pattern

```ts
await queryClient.invalidateQueries({
  queryKey: getUserListQueryKeys(),
});
```

## Avoid

- 문자열 query key를 직접 반복하지 않는다.
- mutation hook 안에 화면 이동을 숨기지 않는다.
- 실패 시 캐시를 무조건 갱신하지 않는다.
