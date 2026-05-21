# Style Token Rule

스타일은 기본적으로 Tailwind theme token과 utility를 사용한다.
split input의 Design 값을 따른다.

## Files

- `app/style/globals.css`
- `app/style/themes.css`
- `app/style/table.css`
- `app/style/checkbox.css`
- `app/style/editor.css`
- `app/style/utils.ts`

## Tokens

- color token은 split input의 primary/secondary를 반영한다.
- typography는 기본 utility를 쓰되 custom scale이면 입력값을 따른다.
- radius, shadow, chart color는 theme 변수로 관리한다.

## Rules

- class 병합은 `cn()`을 사용한다.
- 임의 색상보다 token 색상을 우선한다.
- 버튼, 카드 등 반복 variant는 cva로 관리한다.
- 전역 CSS는 reset, token, 외부 라이브러리 보정에 제한한다.
