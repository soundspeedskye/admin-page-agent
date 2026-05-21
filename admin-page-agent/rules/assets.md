# Assets Rule

정적 자산은 용도별로 분리한다.

## Structure

```txt
public/
  favicon/
  sample/
src/shared/assets/
  fonts/
  icons/
  images/
```

## Rules

- favicon, sample download 파일은 `public`에 둔다.
- 앱에서 import하는 이미지와 폰트는 `shared/assets`에 둔다.
- SVG 컴포넌트는 `icons/index.ts` registry를 통해 사용한다.
- 이미지 index가 필요하면 `shared/assets/images/index.ts`에서 export한다.
- 폰트 CSS는 `globals.css`에서 import한다.

업로드된 사용자 파일과 앱 번들 asset을 섞지 않는다.
