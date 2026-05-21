# Admin Shell Rule

admin 앱은 private layout을 중심으로 구성한다.

## Required Parts

- sidebar.
- nested navigation.
- content area.
- page header area.
- public sign-in page.
- public sign-up page.
- sign-out action.
- auth/session guard.
- global alert.
- global confirm.
- toaster.

## Rules

- Public auth pages stay outside `PrivateLayout`.
- Private pages are children of `PrivateLayout`.
- Sidebar menu is generated from `Navigation`.
- Parent menu groups children but does not require a list page.
- Child menu must map to one route.
- Content area should support dense table pages.

Layout style follows `style-token.md` and `ui-core.md`.
