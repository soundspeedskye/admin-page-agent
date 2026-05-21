# Domain Slice Rule

도메인은 필요한 책임만 폴더로 나눈다.

## Standard Slice

```txt
domain/
  apis/
  hooks/
  model/
  ui/
  lib/
  index.ts
```

## Responsibilities

- `apis`: 서버 통신 함수.
- `hooks`: query and domain hooks. CUD mutation hooks follow `mutation.md` and live in `features`.
- `model`: dto, schema, filter, option type.
- `ui`: 도메인 전용 컴포넌트.
- `lib`: mapper, formatter, column-defs.
- `index.ts`: 외부 공개 API.

## Naming

- 도메인 폴더는 kebab-case.
- 행위 feature는 `create-users`, `update-users`처럼 동사로 시작한다.
- entity는 `users`, `user-group`처럼 명사로 둔다.
