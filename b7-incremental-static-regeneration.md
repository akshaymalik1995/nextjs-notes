# Incremental Static Regeneration in Next.js

Next.js allows you to create or update static pages after you’ve built your site. Incremental Static Regeneration (ISR) enables you to use static-generation on a per-page basis, without needing to rebuild the entire site. With ISR, you can retain the benefits of static while scaling to millions of pages.

## How Incremental Static Regeneration Works

- When a request is made to a page that was pre-rendered at build time, it will initially show the cached page. Any requests to the page after the initial request and before the revalidate time are also cached and instantaneous.
- After the revalidate time window, the next request will still show the cached (stale) page.
- Next.js triggers a regeneration of the page in the background.
- Once the page generates successfully, Next.js will invalidate the cache and show the updated page. If the background regeneration fails, the old page would still be unaltered.

## How to Implement Incremental Static Regeneration

To implement Incremental Static Regeneration in Next.js, you can use the `getStaticProps` and `getStaticPaths` functions as follows:

```jsx
export async function getStaticProps() {
  const res = await fetch('https://.../posts');
  const posts = await res.json();

  return {
    props: {
      posts,
    },
    revalidate: 10, // In seconds
  };
}

export async function getStaticPaths() {
  const res = await fetch('https://.../posts');
  const posts = await res.json();

  const paths = posts.map((post) => ({
    params: { id: post.id },
  }));

  return { paths, fallback: 'blocking' };
}
```

- `getStaticProps` fetches the data and returns it as props for the component. The `revalidate` option specifies the number of seconds after which the page should be regenerated.
- `getStaticPaths` generates the paths that should be pre-rendered at build time. The `fallback` option specifies whether to server-render pages on-demand if the path doesn't exist.



## Conclusion

Incremental Static Regeneration is a powerful feature for Next.js that allows you to create or update static pages on a per-page basis, without needing to rebuild the entire site. This feature can be useful for e-commerce, marketing pages, blog posts, ad-backed media, and more. By implementing ISR, you can retain the benefits of static while scaling to millions of pages.
