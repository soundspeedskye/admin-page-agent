# Form Hook Rule

폼 상태는 화면 조립 위치인 page 또는 widget에서 만든다.

## Pattern

```ts
const form = useForm({
  resolver: zodResolver(createBannerSchema(t)),
  defaultValues: { title: '', isActive: true },
});
```

## Rules

- form type은 zod schema에서 infer한 타입을 사용한다.
- defaultValues는 모든 필드에 명시한다.
- form id가 필요하면 상수로 분리한다.
- 제출 버튼은 `form={FORM_ID}`로 외부 배치할 수 있다.
- field UI는 feature ui 컴포넌트에 form 객체를 prop으로 넘긴다.

## Error

- 서버 중복 에러는 `form.setError`로 field에 연결한다.
- 전역 실패는 toast 또는 global alert로 표시한다.
