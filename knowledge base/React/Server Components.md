Server Components are rendered into html on the server. This means that:
- the page loads faster
- the bundle size is reduced
- the data can be fetched on the server

Client Components are primary rendered in the browser but with Next.JS we can prerender client components on the server and then hydrate them in the browser on app mount.