# Mock Defaults

enabledWhenSwaggerUnavailable: true
listResponseShape: rows-count
authResponseShape: access-token-user
purpose: visual-understanding
dataRealism: realistic-synthetic
locale: ko-KR
rowCount: 10
privacy: synthetic-only
mswHandlers: optionalTools.msw
persistence: memory
seedDataDirectory: shared/api/mocks/data
storeBoundary: msw
authPersistence: memory
authStoreBoundary: msw

## Rule

- Use these defaults only for Swagger/OpenAPI fallback.
- Fallback covers resource APIs and required admin auth APIs.
- Mock rows are part of visual UI review, not just API plumbing.
- Detailed mock generation follows `rules/mock-data-fallback.md`.
