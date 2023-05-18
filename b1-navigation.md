# Navigation

The `Link` component in Next.js is a React component that extends the HTML `<a>` element to provide prefetching and client-side navigation between routes. It is the primary way to navigate between routes in Next.js.

The `Link` component takes a single mandatory prop: `href`. `href` specifies the path or URL to navigate to. This could be an absolute URL, a relative URL, or a URL object.

Here is an example of how to use the `Link` component:

```
import Link from 'next/link';

export default function Home() {
  return (
    <ul>
      <li>
        <Link href="/about">About us</Link>
      </li>
      <li>
        <Link href="/blog/[slug]">Blog Post</Link>
      </li>
    </ul>
  );
}
```

This code will render a list of links to the `/about` and `/blog/[slug]` pages. When the user clicks on a link, the browser will navigate to the corresponding page.

The `Link` component also has a number of optional props that allow you to customize the navigation behavior. For example, you can use the `as` prop to specify a custom label for the link, and you can use the `rel` prop to specify the relationship between the current page and the linked page.

Here is an example of how to use the `as` and `rel` props:

```
import Link from 'next/link';

export default function Home() {
  return (
    <ul>
      <li>
        <Link href="/about" as="About Us">About us</Link>
      </li>
      <li>
        <Link href="/blog/[slug]" rel="external">Blog Post</Link>
      </li>
    </ul>
  );
}
```

This code will render a list of links to the `/about` and `/blog/[slug]` pages. The link to the `/about` page will have the label "About Us", and the link to the `/blog/[slug]` page will have the `rel="external"` attribute, which will tell the browser to open the link in a new tab.

The `Link` component is a powerful tool that can be used to navigate between pages in Next.js applications. It provides a number of features that can improve the performance and user experience of your application, such as prefetching and client-side navigation.
