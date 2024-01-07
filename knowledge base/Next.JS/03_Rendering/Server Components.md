This components can be **rendered and cached on the server**. There are three main **rendering strategies**:

- Static rendering
- Dynamic rendering
- Streaming

By default Next.JS uses server components. There are couple of benefits to doing the rendering work on the server:

- **Date Fetching** - you can fetch date on the server;
- **Security** - keep your sensitive data on the server;
- **Caching** - the render result can be reused between users;
- **Bundle Size** - keep large dependencies on the server;
- **Initial Page Load and First Contentful Paint** - Next.JS gives the user HTML snapshot with data and then hydrate it with interactions;
- **Search Engine Optimization** - no comments;
- **Streaming** - big pages can be split into chunks and sent to the client as they become ready.


## How Server Components are rendered?

On the server, Next.js uses React's APIs to orchestrate rendering. The rendering work is split into chunks: by individual route segments and [Suspense Boundaries](https://react.dev/reference/react/Suspense).

Each chunk is rendered in two steps:

1. React renders Server Components into a special data format called the **React Server Component Payload (RSC Payload)**.
2. Next.js uses the RSC Payload and Client Component JavaScript instructions to render **HTML** on the server.

Then, on the client:

1. The HTML is used to immediately show a fast non-interactive preview of the route - this is for the initial page load only.
2. The React Server Components Payload is used to reconcile the Client and Server Component trees, and update the DOM.
3. The JavaScript instructions are used to [hydrate](https://react.dev/reference/react-dom/client/hydrateRoot) Client Components and make the application interactive.



## Rendering Strategies

### Static Rendering (default)

With Static Rendering, routes are rendered at **build time**, or in the background after [data revalidation](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating#revalidating-data). The result is cached and can be pushed to a [Content Delivery Network (CDN)](https://developer.mozilla.org/docs/Glossary/CDN). This optimization allows you to share the result of the rendering work between users and server requests.


### Dynamic Rendering

With Dynamic Rendering, routes are rendered for each user at **request time**.

Next.JS switches to dynamic rendering when the route contains any information what can be known only in request time or personalized to the user - **dynamic functions or uncached data**.

In Next.JS these dynamic functions are:

- `cookies()` and `headers()`
- `searchParams` in pages / layout props
- `useSearchParams()`
	- In Client Components, it'll skip static rendering and instead render all Client Components up to the nearest parent Suspense boundary on the client.
	- We recommend wrapping the Client Component that uses `useSearchParams()` in a `<Suspense/>` boundary. This will allow any Client Components above it to be statically rendered. [Example](https://nextjs.org/docs/app/api-reference/functions/use-search-params#static-rendering).



### Streaming

Streaming allows to use progressive rendering on the server. Work is split into chunks and sent to the client as it becomes ready. It allows user to see parts of the page immediately.

You can start streaming route segments using `loading.js` and UI components with [React Suspense](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming). See the [Loading UI and Streaming](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming) section for more information.