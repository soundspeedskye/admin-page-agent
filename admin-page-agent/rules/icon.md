# Icon Rule

아이콘은 lucide 또는 SVG registry를 사용한다.

## SVG Registry

- 파일 위치: `shared/assets/icons`
- export 위치: `shared/assets/icons/index.ts`
- import 형식: `./name.svg?react`
- 사용 형식: `Icons.Search` component with `className="size-7"`

## Rules

- 새 SVG는 kebab-case 파일명으로 추가한다.
- registry 객체에 PascalCase 이름으로 등록한다.
- `IconName = keyof typeof Icons` 타입을 유지한다.
- 일반 아이콘 버튼은 lucide에 있으면 lucide를 우선 고려한다.
- 브랜드/제품 고유 아이콘은 SVG registry에 둔다.

inline svg를 JSX 안에 직접 길게 넣지 않는다.
