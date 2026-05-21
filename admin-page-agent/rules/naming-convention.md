# Naming Convention Rule

## Files

- 폴더: `kebab-case`
- API/model/hook/lib 파일: `kebab-case`
- React 컴포넌트 파일: `PascalCase.tsx`
- Storybook 파일: `component.stories.tsx`
- Test 파일: `target.test.ts`

## Code

- 컴포넌트: `PascalCase`
- hook: `useSomething`
- API 함수: `camelCase`
- 타입과 인터페이스: `PascalCase`
- 상수: `UPPER_SNAKE_CASE` 또는 domain query key factory.

## Suffix

- DTO: `SomethingDto`
- Zod schema type: `SomethingSchema`
- list params: `SomethingListParamsDto`
- mapper: `schemaToDtoMapper`

오타가 있는 파일명은 새 코드에서 반복하지 않는다.
