Client Components allows you to write interactive UI that can be rendered on the client at request time.

There are a couple of benefits to doing the rendering work on the client, including:

- **Interactivity**: Client Components can use state, effects, and event listeners, meaning they can provide immediate feedback to the user and update the UI.
- **Browser APIs**: Client Components have access to browser APIs, like [geolocation](https://developer.mozilla.org/docs/Web/API/Geolocation_API) or [localStorage](https://developer.mozilla.org/docs/Web/API/Window/localStorage), allowing you to build UI for specific use cases.

You can define a client component by placing `'use client'` at the top of the file. This means this component and all it's children become client components.



## How are Client Components rendered?

In Next.js, Client Components are rendered differently depending on whether the request is part of a **full page load** (an initial visit to your application or a page reload triggered by a browser refresh) or a **subsequent navigation**.

### Full page load

To optimize the initial page load, Next.js will use React's APIs to render a static HTML preview on the server for both Client and Server Components. This means, when the user first visits your application, they will see the content of the page immediately, without having to wait for the client to download, parse, and execute the Client Component JavaScript bundle.

On the server:

1. React renders Server Components into a special data format called the **React Server Component Payload (RSC Payload)**, which includes references to Client Components.
2. Next.js uses the RSC Payload and Client Component JavaScript instructions to render **HTML** for the route on the server.

Then, on the client:

1. The HTML is used to immediately show a fast non-interactive initial preview of the route.
2. The React Server Components Payload is used to reconcile the Client and Server Component trees, and update the DOM.
3. The JavaScript instructions are used to [hydrate](https://react.dev/reference/react-dom/client/hydrateRoot) Client Components and make their UI interactive.


### Subsequent Navigations

On subsequent navigations, Client Components are rendered entirely on the client, without the server-rendered HTML.