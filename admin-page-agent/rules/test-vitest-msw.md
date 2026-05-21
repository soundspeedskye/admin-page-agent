# Test Vitest MSW Rule

테스트는 Vitest를 기본으로 하고 MSW는 선택 도구로 둔다.

## Unit

- 파일명은 `*.test.ts` 또는 `*.test.tsx`.
- 환경은 node를 기본으로 한다.
- setup은 `src/test/setup-tests.ts`.
- API 로직, mapper, filter, schema를 우선 테스트한다.

## MSW Optional

- `optionalTools.msw`가 true일 때만 구성한다.
- worker는 `shared/api/mocks/browser.ts`.
- handler는 `shared/api/mocks/handlers` 아래 도메인별로 둔다.

## Fallback Handlers

- mock fallback이 active이고 `optionalTools.msw`가 true이면 resource mock data에서 MSW handlers를 생성한다.
- `optionalTools.msw`가 false이면 mock fallback이 active여도 MSW files를 생성하지 않는다.
- list handler를 먼저 생성한다.
- CRUD handlers는 enabled CRUD actions에 대해서만 생성한다.

## Storybook Test

- `optionalTools.storybook`이 true일 때만 구성한다.
- Storybook Vitest project는 Playwright Chromium headless를 사용한다.
- UI regression 전 단계로 story 렌더링을 확인한다.
