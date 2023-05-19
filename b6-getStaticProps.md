# getStaticProps

If you export a function called getStaticProps (Static Site Generation) from a page, Next.js will pre-render this page at build time using the props returned by getStaticProps.

```jsx
export async function getStaticProps(context) {
  return {
    props: {}, // will be passed to the page component as props
  };
}
```
> Note that irrespective of rendering type, any props will be passed to the page component and can be viewed on the client-side in the initial HTML. This is to allow the page to be hydrated correctly. Make sure that you don't pass any sensitive information that shouldn't be available on the client in `props`.


## When should I use getStaticProps?

You should use `getStaticProps` if:
* The data required to render the page is available at build time ahead of a user’s request
* The data comes from a headless CMS
* The page must be pre-rendered (for SEO) and be very fast — `getStaticProps` generates HTML and JSON files, both of which can be cached by a CDN for performance
* The data can be publicly cached (not user-specific). This condition can be bypassed in certain specific situation by using a Middleware to rewrite the path.

## When does getStaticProps run

* getStaticProps always runs during next build
* getStaticProps runs in the background when using fallback: true
* getStaticProps is called before initial render when using fallback: blocking
* getStaticProps runs in the background when using revalidate
* getStaticProps runs on-demand in the background when using revalidate()

When combined with Incremental Static Regeneration, getStaticProps will run in the background while the stale page is being revalidated, and the fresh page served to the browser.

getStaticProps does not have access to the incoming request (such as query parameters or HTTP headers) as it generates static HTML. If you need access to the request for your page, consider using Middleware in addition to getStaticProps.

## Using getStaticProps to fetch data from a CMS

The following example shows how you can fetch a list of blog posts from a CMS.

```jsx

// posts will be populated at build time by getStaticProps()
export default function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  );
}
 
// This function gets called at build time on server-side.
// It won't be called on client-side, so you can even do
// direct database queries.
export async function getStaticProps() {
  // Call an external API endpoint to get posts.
  // You can use any data fetching library
  const res = await fetch('https://.../posts');
  const posts = await res.json();
 
  // By returning { props: { posts } }, the Blog component
  // will receive `posts` as a prop at build time
  return {
    props: {
      posts,
    },
  };
}

```

## Write server-side code directly

As getStaticProps runs only on the server-side, it will never run on the client-side. It won’t even be included in the JS bundle for the browser, so you can write direct database queries without them being sent to browsers.

This means that instead of fetching an API route from getStaticProps (that itself fetches data from an external source), you can write the server-side code directly in getStaticProps.

The logic for fetching the data from the CMS can be shared by using a lib/ directory. Then it can be shared with getStaticProps.

```jsx
// The following function is shared
// with getStaticProps and API routes
// from a `lib/` directory
export async function loadPosts() {
  // Call an external API endpoint to get posts
  const res = await fetch('https://.../posts/');
  const data = await res.json();
 
  return data;
}
 
// pages/blog.js
import { loadPosts } from '../lib/load-posts';
 
// This function runs only on the server side
export async function getStaticProps() {
  // Instead of fetching your `/api` route you can call the same
  // function directly in `getStaticProps`
  const posts = await loadPosts();
 
  // Props returned will be passed to the page component
  return { props: { posts } };
}
```

## Statically generates both HTML and JSON
When a page with getStaticProps is pre-rendered at build time, in addition to the page HTML file, Next.js generates a JSON file holding the result of running getStaticProps.

This JSON file will be used in client-side routing through `next/link` or `next/router`.

When you navigate to a page that’s pre-rendered using getStaticProps, Next.js fetches this JSON file (pre-computed at build time) and uses it as the props for the page component. This means that client-side page transitions will not call getStaticProps as only the exported JSON is used.

When using Incremental Static Generation, getStaticProps will be executed in the background to generate the JSON needed for client-side navigation. You may see this in the form of multiple requests being made for the same page, however, this is intended and has no impact on end-user performance.


## Where can I use getStaticProps

getStaticProps can only be exported from a page. You cannot export it from non-page files, `_app`, `_document`, or `_error`.

One of the reasons for this restriction is that React needs to have all the required data before the page is rendered.

Also, you must use export getStaticProps as a standalone function — it will not work if you add getStaticProps as a property of the page component.

## Runs on every request in development
In development (next dev), getStaticProps will be called on every request.

## Configuration Options

Here are the configuration options available in `getStaticProps`:

- `revalidate`: This option is used to enable ISR and sets the time (in seconds) to re-generate the page after the initial build. For example, `{ revalidate: 60 }` will re-generate the page every 60 seconds. [Source 0](https://nextjs.org/docs/basic-features/data-fetching), [Source 1](https://stackoverflow.com/questions/66165707/nextjs-getstaticprops-revalidate-not-working), [Source 4](https://stackoverflow.com/questions/62701494/next-js-getstaticprops-not-updating-fetch-values-in-production)
- `notFound`: This option is used to return a 404 page when the data being fetched by `getStaticProps` is not found. For example, `{ notFound: true }` will return a 404 page. [Source 0](https://nextjs.org/docs/basic-features/data-fetching)
- `redirect`: This option is used to redirect the user to another page when the data being fetched by `getStaticProps` is not found. For example, `{ redirect: { destination: '/', permanent: false } }` will redirect the user to the homepage. [Source 0](https://nextjs.org/docs/basic-features/data-fetching)

To use these options, they can be added to the object returned by `getStaticProps`. For example:

```jsx
export async function getStaticProps(context) {
  // fetch data
  const data = await fetch('/api/data');
  
  // return data and configuration options
  return {
    props: { data },
    revalidate: 60,
    notFound: true,
    redirect: { destination: '/', permanent: false }
  }
}
```

Note that `revalidate` only works when the Next.js server is running. When using `next export` to generate static files, ISR will not work. [Source 1](https://stackoverflow.com/questions/66165707/nextjs-getstaticprops-revalidate-not-working), [Source 3](https://www.reddit.com/r/nextjs/comments/lyg4ci/revalidate_on_getstaticprops_does_not_trigger/)


