# Format And Lint

포맷과 린트는 ESLint flat config와 Prettier 조합을 사용한다.

## Prettier

```json
{
  "singleQuote": true,
  "semi": true,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80
}
```

## Tailwind

- `prettier-plugin-tailwindcss`를 사용한다.
- `tailwindFunctions`는 `cva`, `cn`을 포함한다.

## ESLint

- `@eslint/js`
- `typescript-eslint`
- `eslint-plugin-react-hooks`
- `eslint-plugin-react-refresh`
- `eslint-config-prettier`
- `eslint-plugin-prettier`

## Rules

- `prettier/prettier`는 error로 둔다.
- React hooks recommended rules를 켠다.
- `react-refresh/only-export-components`는 warn으로 둔다.
- story 파일과 dist는 lint 대상에서 제외한다.
