Here's a quick summary of the different use cases for Server and Client Components:

|What do you need to do?|Server Component|Client Component|
|---|---|---|
|Fetch data|||
|Access backend resources (directly)|||
|Keep sensitive information on the server (access tokens, API keys, etc)|||
|Keep large dependencies on the server / Reduce client-side JavaScript|||
|Add interactivity and event listeners (`onClick()`, `onChange()`, etc)|||
|Use State and Lifecycle Effects (`useState()`, `useReducer()`, `useEffect()`, etc)|||
|Use browser-only APIs|||
|Use custom hooks that depend on state, effects, or browser-only APIs|||
|Use [React Class components](https://react.dev/reference/react/Component)|||


## Server Components

### Sharing data between components

As React Context is not available on the server you can use [`fetch`](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating#fetching-data-on-the-server-with-fetch) or React's `cache` function to fetch the same data in the components that need it, without worrying about making duplicate requests for the same data. This is because React extends `fetch` to automatically memoize data requests, and the `cache` function can be used when `fetch` is not available.


### Keeping Server-only Code out of the Client Environment

Use `server-only` package to throw error when server-only file is imported into client component.



## Client Components

### Moving Client Components Down the Tree

To reduce the Client JavaScript bundle size, we recommend moving Client Components down your component tree.

For example, you may have a Layout that has static elements (e.g. logo, links, etc) and an interactive search bar that uses state.

Instead of making the whole layout a Client Component, move the interactive logic to a Client Component (e.g. <SearchBar />) and keep your layout as a Server Component. This means you don't have to send all the component Javascript of the layout to the client.


## [Interleaving Server and Client Components](https://nextjs.org/docs/app/building-your-application/rendering/composition-patterns#interleaving-server-and-client-components)

When interleaving Client and Server Components, it may be helpful to visualize your UI as a tree of components. Starting with the [root layout](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#root-layout-required), which is a Server Component, you can then render certain subtrees of components on the client by adding the `"use client"` directive.

Within those client subtrees, you can still nest Server Components or call Server Actions, however there are some things to keep in mind:

- During a request-response lifecycle, your code moves from the server to the client. If you need to access data or resources on the server while on the client, you'll be making a **new** request to the server - not switching back and forth.
- When a new request is made to the server, all Server Components are rendered first, including those nested inside Client Components. The rendered result (RSC Payload) will contain references to the locations of Client Components. Then, on the client, React uses the RSC Payload to reconcile Server and Client Components into a single tree.

- Since Client Components are rendered after Server Components, you cannot import a Server Component into a Client Component module (since it would require a new request back to the server). Instead, you can pass a Server Component as `props` to a Client Component. See the [unsupported pattern](https://nextjs.org/docs/app/building-your-application/rendering/composition-patterns#unsupported-pattern-importing-server-components-into-client-components) and [supported pattern](https://nextjs.org/docs/app/building-your-application/rendering/composition-patterns#supported-pattern-passing-server-components-to-client-components-as-props) sections below.