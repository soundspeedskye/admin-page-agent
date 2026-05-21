# Storybook Rule

공용 UI와 primitive는 Storybook으로 확인한다.

## Config

- framework: `@storybook/react-vite`
- stories: `src/**/*.mdx`, `src/**/*.stories.*`
- addons: docs, onboarding, a11y, vitest.
- chromatic은 `optionalTools.chromatic: true`일 때만 추가한다.
- preview에서 `src/app/style/globals.css`를 import한다.

## Rules

- story 파일은 컴포넌트 근처 또는 `shared/ui/stories`에 둔다.
- control matcher는 color와 date를 기본 제공한다.
- a11y test는 초기에는 `todo`로 둔다.
- UI library 변경 시 Storybook에서 시각 확인한다.

업무 도메인 페이지보다 재사용 UI story를 우선 만든다.
