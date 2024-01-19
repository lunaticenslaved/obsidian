There are two ways to navigate in Next.JS:

- with `<Link />` component
- with `useRouter`

But `useRouter` can be used only on client side. On the server should be used `redirect`.


### How Routing and Navigation Works

The App Router uses hybrid approach to navigation: the code is splitted by route segments. On the client side Next.JS prefetches and cache route segments. When a user navigates to new page, the browser does not reload the page. It only rerenders the segment that was changed.

##### 1. Code Splitting

Route segments are authomitically splitted into smaller bundles to be downloaded and executed by the browser.

##### 2. Prefetching

Prefetching is the way to preload the route before the user visits it.

The are two ways the route is prefetched is Next.JS:

- `<Link />` component: routes are prefetched when they become visible in the viewer's viewport. You can disable prefetching by setting `prefetch={false}` prop. Static and dynamic routes are prefetched differently:
	- **Static Routes**: prefetch default to `true`
	- **Dynamic Routes**: prefetch default to `authomatic`. Only the shared layout, down the rendered "tree" of components until the first `loading.js` file, is prefetched and cached for `30s`. This reduces the cost of fetching an entire dynamic route, and it means you can show an [instant loading state](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming#instant-loading-states) for better visual feedback to users.
- `router.prefetch()`: the route can be prefetched programmatically.

**Prefetching is not enabled in development. Only in production.**

##### 3. Caching

Next.js has an **in-memory client-side cache** called the [Router Cache](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating#caching-data#router-cache). As users navigate around the app, the React Server Component Payload of [prefetched](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#2-prefetching) route segments and visited routes are stored in the cache.

This means on navigation, the cache is reused as much as possible, instead of making a new request to the server - improving performance by reducing the number of requests and data transferred.

##### 4. Partial Rendering

Partial rendering means only the route segments that change on navigation re-render on the client, and any shared segments are preserved.

##### 5. Soft Navigation

Browsers perform a "hard navigation" when navigating between pages. The Next.js App Router enables "soft navigation" between pages, ensuring only the route segments that have changed are re-rendered (partial rendering). This enables client React state to be preserved during navigation.

##### 6. Back and Forward Navigation

By default, Next.js will maintain the scroll position for backwards and forwards navigation, and re-use route segments in the [Router Cache](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating#caching-data).