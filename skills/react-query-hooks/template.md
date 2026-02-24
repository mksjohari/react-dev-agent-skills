# React Query Hooks - Code Templates

## useQuery hook pattern

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

## useMutation hook pattern with invalidation

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

## types.ts pattern

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

## transformer.ts pattern with select

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

## Folder structure

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
