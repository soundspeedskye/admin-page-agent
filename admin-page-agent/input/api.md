# API

baseUrlEnv:
swaggerUrl:

## Rule

- `swaggerUrl` is optional.
- If `swaggerUrl` is empty, skip OpenAPI fetch/read and generate from `input/resources/*.md`, `input/auth.md`, and mock fallback.
- `baseUrlEnv` can be defined before the real API server exists; it is the future runtime env key, not proof that the API is available.
