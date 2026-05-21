# API Convention Rule

모든 HTTP 호출은 `shared/api/request.ts`의 typed `request` wrapper를 사용한다.

## Request Shape

```ts
request({
  method: 'get',
  url: '/api/admin/users',
  queryParams,
  requestBody,
  config,
});
```

## Rules

- GET은 `queryParams`를 사용한다.
- POST/PUT/PATCH는 `requestBody`를 사용한다.
- DELETE에 body가 필요하면 wrapper의 delete data 규칙을 따른다.
- Auth API 함수도 같은 request wrapper를 사용한다.
- API 함수는 response data를 그대로 반환하거나 필요한 row만 명확히 반환한다.
- endpoint 문자열은 API 함수 안에만 둔다.

## Error

- 403은 forbidden 이동 규칙을 따른다.
- 500은 server-error 이동 규칙을 따른다.
- 서버 error body는 `APIErrorResponse`로 throw한다.
