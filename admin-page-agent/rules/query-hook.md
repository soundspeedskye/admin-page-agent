# Query Hook Rule

조회 hook은 `entities/{domain}/hooks`에 둔다.

## Pattern

```ts
export const useBannerListQuery = (
  params: BannerListParamsDto,
  options?: { enabled?: boolean },
) =>
  useQuery({
    queryKey: getBannerListQueryKeys(params),
    queryFn: () => getBannerList(params),
    placeholderData: keepPreviousData,
    enabled: options?.enabled,
  });
```

## Rules

- list query는 `keepPreviousData`를 기본으로 고려한다.
- enabled가 필요한 경우 options 객체로 받는다.
- API 함수와 query key factory를 분리한다.
- hook 이름은 `use{Domain}{List|Detail}Query`.
- suspense가 필요하면 별도 query options factory를 만든다.

query hook 안에서 UI side effect를 실행하지 않는다.
