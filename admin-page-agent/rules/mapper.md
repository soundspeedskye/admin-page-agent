# Mapper Rule

폼 값과 서버 DTO가 다르면 mapper를 둔다.

## Location

- `features/{action-domain}/lib/mapper.ts`
- 조회 데이터 변환은 `entities/{domain}/lib/mapper.ts`

## Pattern

```ts
export const createUserSchemaToCreateUserDtoMapper = (
  data: CreateUserSchema,
): CreateUserDto => ({
  name: data.name,
  avatarFileId: data.avatarFile?.id ?? '',
});
```

## Rules

- 날짜 ISO 변환은 mapper에서 한다.
- media 객체를 id로 바꾸는 작업도 mapper에서 한다.
- form component는 DTO 구조를 알지 않는다.
- API 함수는 form schema를 직접 받지 않는다.

mapper 이름은 source와 target을 모두 드러낸다.
