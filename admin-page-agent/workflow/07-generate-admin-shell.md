# 07 Generate Admin Shell

공통 admin 화면 골격을 생성한다.

## Generate

- app providers.
- `PrivateLayout`.
- sidebar UI using the navigation menu model from `04-navigation-map.md`.
- page content area.
- global alert and confirm.
- toaster.
- public sign-in page.
- public sign-up page.
- sign-out action.
- auth token/session storage.
- private auth guard implementation.

## Core Artifact Reuse

- Follow `rules/ui-core.md` `Verified Core Artifact Baseline` before generating `shared/ui/core` components.
- Reuse matching verified core artifacts during shell generation.
- If no matching verified artifact exists, generate the needed core component and let `09-review-and-verify.md` decide whether it can be promoted.

## Layout Requirements

- Sidebar is consistent across private routes.
- Parent category expands to child menu.
- Active child route is visually selected.
- Content area supports list pages without layout shift.
- Header area can host page title and actions.

## Rules

Use `admin-shell.md`, `sidebar-navigation.md`, `private-route-guard.md`, `auth-generation.md`, `auth-token-storage.md`, and `ui-core.md`.
