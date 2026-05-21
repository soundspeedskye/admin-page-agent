# UI Kit Rule

기본 UI primitive는 split input의 `uiKit` 값을 기준으로 선택한다.

## Location

- kit primitive wrapper: `shared/ui/lib`
- 업무 공통 wrapper: `shared/ui/core`

## Rules

- `uiKit`에 지정된 라이브러리를 설치하고 공식 문서의 primitive, import path, provider, theme 설정을 따른다.
- 알려진 kit과 `uiKit: none`은 `uiKitSource: auto`, `uiKitProvider: auto`일 때 admin-page-agent의 기본 매핑을 사용한다.
- Button, Input, Select, Form, Dialog, Sheet, Card 등 기본 primitive는 `shared/ui/lib`에서 import할 수 있게 정리한다.
- 업무 화면은 외부 UI kit을 직접 흩뿌리지 말고 `shared/ui/lib` 또는 `shared/ui/core`를 통해 사용한다.
- `uiKitTheme` 값은 선택한 kit의 theme 설정에만 반영한다.
- kit이 제공하는 접근성 primitive와 keyboard interaction을 유지한다.
- 새 primitive가 필요하면 선택한 kit의 variant, token, style override 방식을 따른다.

## Kit Specific Notes

- `uiKit: shadcn`이면 shadcn/Radix 컴포넌트를 `shared/ui/lib`에 생성하고 `uiKitTheme`의 `baseColor`를 `components.json`에 반영한다.
- `uiKit: mui`, `antd`, `chakra`, `mantine` 등 외부 패키지 기반 kit이면 공식 package, provider, CSS reset, theme provider 설정을 먼저 반영한다.
- `uiKit: custom`이면 `uiKitSource`의 외부 primitive source 또는 local alias와 `uiKitProvider`의 provider 규칙을 확인한다. 생성되는 adapter 위치는 `shared/ui/lib`로 고정한다.
- `uiKit: none`이면 외부 UI kit primitive를 설치하지 않고 프로젝트 token과 HTML semantic element를 기반으로 최소 wrapper만 둔다.

## Avoid

- 같은 역할의 primitive를 페이지 안에서 새로 만들지 않는다.
- 도메인 전용 문구를 `shared/ui/lib`에 넣지 않는다.
- split input에 없는 UI kit을 임의로 선택하지 않는다.
