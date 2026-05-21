# 00 Bootstrap Project

빈 프로젝트 또는 최소 init 프로젝트를 admin 앱으로 시작할 수 있게 준비한다.

## Detect

1. `package.json`이 있는지 확인한다.
2. `vite.config.ts`가 있는지 확인한다.
3. `src/main.tsx`, `src/App.tsx`, `index.html`이 있는지 확인한다.
4. 이미 앱이 있으면 기존 구조를 보존하고 누락된 파일만 만든다.
5. 완전 빈 폴더면 Vite React TS 구조를 생성한다.

## Create If Missing

- `package.json`, `index.html`.
- `tsconfig.json`, `tsconfig.app.json`, `tsconfig.node.json`.
- `vite.config.ts`, `eslint.config.js`, `.prettierrc`.
- `src/main.tsx`, `src/App.tsx`, `src/vite-env.d.ts`.

## Create Directories

- `src/app/{i18n,provider,routing,style,ui}`.
- `src/{pages,widgets,features,entities}`.
- `src/shared/{api,assets,hooks,lib,model,store,ui}`.
- `src/shared/ui/{core,lib}`.
- Do not create empty domain or action subfolders during bootstrap.

## Install Dependencies

- Detect package manager from lockfile.
- No lockfile means ask user or default to yarn.
- Before install, show package manager and package list.
- Ask for approval before running network install commands.
- Install required packages from `01-package-baseline.md` after approval.
- Install optional packages only when enabled in split input.

## Rules

- Do not overwrite existing app files without reading them first.
- Preserve existing user code.
- Prefer filling missing config over replacing entire files.
- Match aliases, Vite settings, and formatting baseline docs.

## Done When

- React entry files exist.
- FSD directories exist.
- dev, build, lint scripts exist.
- TypeScript and Vite aliases match.
- app can render a placeholder page.
