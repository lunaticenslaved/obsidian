### Fetch data on the server

Prefer fetching on the server over fetching on the client.


### Streaming

Streaming and Suspense are used to progressively render the application and send in to the client in parts.


### Parallel and sequential data fetching

![[Pasted image 20240120195723.png]]


### [Preloading Data](https://nextjs.org/docs/app/building-your-application/data-fetching/patterns#preloading-data)

You can create `preload` function to use it in server component.


### Using `cache`, `server-only` and preloading

With combination of these tools you can create a function with ability to preload and cache data and can be used only on the server.


### Preventing sensitive data from being exposed to the client

We recommend using React's taint APIs, [`taintObjectReference`](https://react.dev/reference/react/experimental_taintObjectReference) and [`taintUniqueValue`](https://react.dev/reference/react/experimental_taintUniqueValue), to prevent whole object instances or sensitive values from being passed to the client.

Usage of any taint data will cause on error.