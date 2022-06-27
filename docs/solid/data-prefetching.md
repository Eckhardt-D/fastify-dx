<sub>**Go back to the [index](https://github.com/fastify/fastify-dx/blob/main/packages/fastify-dx-solid/README.md).**</sub>

<br>

## Isomorphic data prefetching

Fastify DX for Svelte implements the `getData()` hook from the [URMA specification](https://github.com/fastify/fastify-dx/blob/main/URMA.md) to solve this problem.

### `getData(ctx)`

This hook is set up in a way that it runs server-side before any SSR takes place, so any data fetched is made available to the route component before it starts rendering. During first render, any data retrieved on the server is automatically sent to be hydrated on the client so no new requests are made. Then, during client-side navigation (post first-render), a JSON request is fired to an endpoint automatically registered for running the `getData()` function for that route on the server.

The objet returned by `getData()` gets automatically assigned as `data` in the [universal route context](https://github.com/fastify/fastify-dx/blob/main/docs/svelte/route-context.md) object and is accessible from `getMeta()` and `onEnter()` hooks and also via the `useRouteContext()` hook.

```jsx
import { useRouteContext } from '/dx:core.js'

export function getData (ctx) {
  return {
    message: 'Hello from getData!',
  }
}

export default function Route (props) {
  const { data } = useRouteContext()
  return <p>{data.message}</p>
}
```
