# React Query Hooks - Examples

## useQuery: Fetching data

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

## useMutation: Mutating data

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
