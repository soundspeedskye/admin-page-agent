# TypeScript Baseline

TypeScript는 strict하고 bundler 친화적으로 설정한다.

## Root `tsconfig.json`

- project references를 사용한다.
- `tsconfig.app.json`, `tsconfig.node.json`로 분리한다.
- `baseUrl`은 `.`로 둔다.
- alias는 `src` 계층과 1:1로 맞춘다.

## Path Alias

```json
"@/*": ["./src/*"],
"@app/*": ["./src/app/*"],
"@entities/*": ["./src/entities/*"],
"@features/*": ["./src/features/*"],
"@shared/*": ["./src/shared/*"]
```

## App Config

- `target`: `ES2022`
- `module`: `ESNext`
- `moduleResolution`: `bundler`
- `jsx`: `react-jsx`
- `strict`: `true`
- `noUnusedLocals`: `true`
- `noUnusedParameters`: `true`
- `noFallthroughCasesInSwitch`: `true`
- `noUncheckedSideEffectImports`: `true`

## Node Config

- Vite config 전용으로 분리한다.
- `target`과 `lib`는 `ES2023` 이상을 사용한다.
- 브라우저 타입을 섞지 않는다.
