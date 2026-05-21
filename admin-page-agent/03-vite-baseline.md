# Vite Baseline

Vite는 React SWC, Tailwind, SVGR, Vitest 설정을 포함한다.

## Plugins

- `@vitejs/plugin-react-swc`
- `@tailwindcss/vite`
- `vite-plugin-svgr`

## Server

- port, host, allowedHosts는 split input의 `devServer`를 따른다.
- 값이 없으면 Vite 기본값을 사용한다.

## Alias

Vite alias는 `tsconfig.json` paths와 반드시 일치시킨다.

## SVG

- SVG 컴포넌트 import는 `*.svg?react`만 허용한다.
- SVGR include는 `**/*.svg?react`로 제한한다.

## Test

- unit test project를 기본으로 둔다.
- Storybook test는 `optionalTools.storybook`이 true일 때만 둔다.
- test setup은 `src/test/setup-tests.ts`에 둔다.
