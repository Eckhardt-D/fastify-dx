
## Universal route enter event

<table>
<tr>
<td width="400px" valign="top">

### `onEnter(ctx)`

If a route module exports a `onEnter()` function, it's executed before the route renders, both in SSR and client-side navigation. That is, the first time a route render on the server, onEnter() runs on the server. Then, since it already ran on the server, it doesn't run again on the client for that first route. But if you navigate to another route on the client using `<Link>`, it runs normally as you'd expect.

It receives the [universal route context](https://github.com/fastify/fastify-dx/blob/main/packages/fastify-dx-react/README.md#route-context) as first parameter, so you can make changes to `data`, `meta` and `state` if needed.

</td>
<td width="600px"><br>

```jsx
export function onEnter (ctx) {
  if (ctx.server?.underPressure) {
    ctx.clientOnly = true
  }
}

export function Index () {
  return <p>No pre-rendered HTML sent to the browser.</p>
}
```

The example demonstrates how to turn off SSR and downgrade to CSR-only, assuming you have a `pressureHandler` configured in [`underpressure`](https://github.com/fastify/under-pressure) to set a `underPressure` flag on your server instance.

</td>
</tr>
</table>
