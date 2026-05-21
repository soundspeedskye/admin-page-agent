# Form Zod Rule

폼 schema는 `features/{action-domain}/model/*.schema.ts`에 둔다.

## Pattern

```ts
export const createUserSchema = (t: TFunction) =>
  z.object({
    name: z.string().min(1, t('common.errors.empty')),
  });
```

## Rules

- i18n 메시지가 필요하면 schema factory가 `t`를 받는다.
- 서버 DTO schema와 form schema를 섞지 않는다.
- cross-field 검증은 `.refine`으로 작성한다.
- refine의 `path`는 실제 form field를 지정한다.
- 공통 schema는 `shared/model`에 둔다.

schema 이름은 action과 domain을 포함한다.
