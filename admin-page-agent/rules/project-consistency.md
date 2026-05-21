# Project Consistency Rule

프로젝트마다 구현 방식은 달라질 수 있다.
하지만 한 프로젝트 안에서는 같은 역할의 UI와 로직을 반복해서 새로 만들지 않는다.

## Rules

- 첫 list page를 만들 때 반복될 구조를 확인한다.
- 두 번째 list page부터는 첫 번째 list page의 구조와 흐름을 기준으로 맞춘다.
- 같은 역할의 header, search, filter, table, pagination은 기존 구현을 재사용한다.
- 기존 공통 컴포넌트가 있으면 새로 만들지 않고 확장한다.
- 같은 역할의 hook, mapper, query key naming은 한 프로젝트 안에서 통일한다.
- 한 resource만을 위한 별도 패턴은 만들지 않는다.
- 예외가 필요하면 이유를 작업 요약에 남긴다.

## Apply To

- app provider
- router
- private layout
- sidebar
- page header
- list page
- search and filter
- table and pagination
- API request
- query and mutation hooks

일관성은 고정된 props 강제가 아니라 기존 프로젝트 패턴 재사용으로 유지한다.
