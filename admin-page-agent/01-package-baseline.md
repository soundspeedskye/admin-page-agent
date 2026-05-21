# Package Baseline

아래 스택은 기본값이다. 버전과 선택 도구는 split input 파일에서 읽는다.

## Required Core

- React
- React DOM
- Vite
- TypeScript
- React Router

## Required Styling

- Tailwind CSS
- `@tailwindcss/vite`
- UI kit dependencies according to `input/stack.md` `uiKit`.
- Theme/provider dependencies required by the selected UI kit

## Conditional UI Kit Packages

- shadcn: shadcn/ui, Radix UI, `class-variance-authority`, `clsx`, `tailwind-merge`
- mui: `@mui/material`, Emotion packages, and required icon/date packages when used
- antd: `antd` and required style reset/theme setup
- chakra: Chakra UI packages and required Emotion/provider setup
- mantine: Mantine packages and required style/provider setup
- none/custom: install only packages explicitly required by split input.

## Required Data

- `@tanstack/react-query`
- Axios
- `qs`
- Zod
- React Hook Form
- `@hookform/resolvers`

## Recommended UI

- `lucide-react`
- `sonner`
- `date-fns`
- `dayjs`
- `i18next`
- `react-i18next`
- `zustand`

## Required Tooling

- ESLint flat config
- Prettier
- `prettier-plugin-tailwindcss`
- Vitest

## Optional

- AG Grid when `tableLibrary: ag-grid`.
- UI kit packages when `uiKit` is not `none`.
- Storybook when `optionalTools.storybook: true`.
- Chromatic when `optionalTools.chromatic: true`.
- MSW when `optionalTools.msw: true`.
- Playwright when `optionalTools.playwright: true`.
