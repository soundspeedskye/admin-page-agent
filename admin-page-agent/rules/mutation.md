# Mutation Rule

생성, 수정, 삭제는 feature hook으로 분리한다.

## Pattern

```ts
export const useCreateBannerMutation = (options?: MutationOptions) => {
  const queryClient = useQueryClient();
  const { onSuccess, ...restOptions } = options ?? {};

  return useMutation({
    mutationFn: createBanner,
    ...restOptions,
    onSuccess: async (data, variables, mutateResult, context) => {
      await queryClient.invalidateQueries({
        queryKey: getBannerListQueryKeys(),
      });
      await onSuccess?.(data, variables, mutateResult, context);
    },
  });
};
```

## Rules

- API 함수는 `features/{action-domain}/apis`에 둔다.
- mutation hook은 `features/{action-domain}/hooks`에 둔다.
- mutation hook은 기본 mutationFn과 관련 query invalidation을 제공한다.
- mutation hook은 optional `UseMutationOptions`를 받는다.
- mutation hook은 사용자 제공 `onSuccess`를 options spread 전에 분리한다.
- mutation hook은 성공 시 관련 list/detail query key를 `queryClient.invalidateQueries`로 무효화한다.
- 내부 invalidation은 사용자 제공 `onSuccess`보다 먼저 실행한다.
- CRUD 반영의 기본 전략으로 `queryClient.setQueryData`를 사용하지 않는다.
- 하나의 feature 폴더는 하나의 사용자 mutation action만 책임진다.
- create, update, delete를 `features/resource-crud` 같은 단일 폴더에 합치지 않는다.

## Foldering

Resource CRUD를 생성할 때는 resource별 action feature 폴더로 분리한다.
`create-resource-row`, `update-resource-row`, `delete-resource-row`처럼 모든 resource를
공유하는 generic row mutation feature를 만들지 않는다.

```txt
features/create-{resource}/
  apis/create-{resource}.ts
  hooks/use-create-{resource}-mutation.ts
  model/create-{resource}.schema.ts
  index.ts

features/update-{resource}/
  apis/update-{resource}.ts
  hooks/use-update-{resource}-mutation.ts
  model/update-{resource}.schema.ts
  index.ts

features/delete-{resource}/
  apis/delete-{resource}.ts
  hooks/use-delete-{resource}-mutation.ts
  index.ts
```

## Naming

- `useCreateXMutation`
- `useUpdateXMutation`
- `useDeleteXMutation`
- bulk 작업은 `Bulk`를 이름에 포함한다.
