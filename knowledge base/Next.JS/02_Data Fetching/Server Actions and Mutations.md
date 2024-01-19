Server Actions are async functions that are executed on the server. They can be used on the client and on the server.

### Server Components

Use can define server actions in Server Components using `use server` directive.

### Client Components

Use can use server actions in Client Components only by importing actions from a file with `use server` directive.

### Behavior

- You can use server action in form's `action` prop.
- Use as function use `useEffect` or `useCallback` or other.
- Server Actions is integrated with caching and revalidating behavior so they can return both data and updated interface in response.
- Server Actions use `POST` method.
- Both request and response must be serializable.
- Server Actions inherit the [runtime](https://nextjs.org/docs/app/building-your-application/rendering/edge-and-nodejs-runtimes) from the page or layout they are used on.

### Protection

By default Server Actions can invoked on the same host as the page that hosts it. It can be changed in `next.config` file with `serverActions.allowedOrigins` option.