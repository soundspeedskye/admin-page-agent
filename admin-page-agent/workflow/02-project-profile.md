# 02 Project Profile

프로젝트별 설정을 코드 설정으로 옮긴다.

## Read

- `input/project.md`
- `input/stack.md`
- `input/design.md`
- `input/api.md`
- `input/auth.md`

## Generate Or Update

- `package.json` scripts, dependencies, optional tools.
- `tsconfig.json` aliases.
- `vite.config.ts` plugins, alias, server.
- UI kit setup from `uiKit`: dependencies, provider, theme config, component aliases or wrappers.
- `app/style/themes.css` color and typography token.
- `app/i18n` default language.

## Rules

- Follow `style-token.md`.
- Follow `ui-kit.md`.
- Follow `api-convention.md`.
- Keep project-specific values in code, not in workflow docs.
