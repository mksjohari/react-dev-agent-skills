---
name: react-query-hooks
description: TanStack Query (React Query) hook conventions. Use when writing API calls, useQuery hooks, useMutation hooks, query keys, axios requests, or data fetching/mutating hooks in React.
user-invocable: false
---

# API calls in React

Always use Tanstack Query to fetch data in React applications. It handles all the complexities of fetching, caching, syncronizing and updating server state. For all logical groupings of hooks related to an API endpoint, the relevant files should live inside a `queries` folder.

For example, if I have multiple different API calls to `/api/client`, then all related query fetching code should go inside a `hooks/queries/client` folder.

## When to use

Use this skill when writing code to fetch / mutate data in React.

## Use the useQuery hook for fetching data

Create a hook to wrap the useQuery hook to fetch the data. The hook name should indicate what data it is fetching. This hook should be inside a `hook.ts` file.

**Incorrect:**

```typescript
useEffect(() => {
  const res = await fetch(`http://example.com/api/client/${clientId}`);
}, []);
```

**Correct:**

```typescript
import { useQuery } from "@tanstack/react-query";

const clientInfoKey = "clientInfoKey";

const getClientInfo = async (clientId: string): Promise<IClientDTO> => {
  const response = await axios.get<IClientDTO>(
    `http://example.com/api/client/${clientId}`,
  );
  return response.data;
};

export const useClientInfo = (clientId: string) => {
  return useQuery({
    queryKey: [clientInfoKey, clientId],
  });
};
```

## Use the useMutation hook for mutating data

Create a hook to wrap the useMutation hook to mutate the data. The hook name should indicate what data it is mutating. Then we should invalidate the related query that queries this data. This hook should be inside a `hook.ts` file.

**Incorrect:**

```typescript
useEffect(() => {
  const res = await fetch(`http://example.com/api/client/${clientId}`, {
    method: "POST",
    body: JSON.stringify({ username: "example" }),
  });
}, []);
```

**Correct:**

```typescript
import { useMutation, useQueryClient } from "@tanstack/react-query";

const clientInfoKey = "clientInfoKey";

const updateClientInfo = async ({
  clientId,
  clientInfo,
}: IUpdateClientInfoRequest): Promise<IClientInfoDTO> => {
  const response = await axios.get<IClientInfoDTO>(
    `http://example.com/api/client/${clientId}`,
    clientInfo,
  );
  return response.data;
};

export const useUpdateClientInfo = () => {
  const queryClient = new QueryClient();

  return useMutation({
    mutationFn: updateClientInfo,
    onSuccess: (_, variables) => {
      queryClient.invalidateQueries({
        queryKey: [clientInfoKey, variables.clientId],
      });
    },
  });
};
```

## Create type file to keep all request and response shapes

Create `types.ts` to keep all the type definitions of request params and response DTOs.

```typescript
// types.ts

export interface IUpdateClientInfoRequest {
  clientId: string;
  clientInfo: IClientInfoDTO;
}

export interface IClientInfoDTO {
  username: string;
  name: string;
  createdTimestamp: string;
}
```

## Create transformer file to map DTO to client useable viewmodel

If the data from API response needs to be transformed to match frontend client use case, create a `transformer.ts` file to do the mapping, and type this transformed shape as a VM. Use this transform function in the `select` param of `useQuery`.

```typescript
// types.ts
export interface IClientInfoVM {
  username: string;
  name: string;
  createdDate: Date;
}

// transformer.ts
const transformClientInfoDTOToVM = (
  clientInfo: IClientInfoDTO,
): IClientInfoVM => {
  return {
    ...clientInfo,
    createdDate: new Date(clientInfo.createdTimestamp),
  };
};

/// hook.ts
export const useClientInfo = (clientId: string) => {
  return useQuery({
    queryKey: [clientInfoKey, clientId],
    select: transformClientInfoDTOToVM,
  });
};
```

## Example complete folder structure of a API hook using Tanstack Query

```
hooks/
  └── queries/
    └── client/
      └── hook.ts // contains the mutations and queries
      └── transformer.ts // contains the transformer functions
      └── types.ts // contains the request and response type definitions
      └── index.ts
    └── index.ts
  └── index.ts

```
