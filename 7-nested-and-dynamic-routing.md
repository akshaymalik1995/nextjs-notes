# Nested and Dynamic Routes

Nested routes in Next.js refer to the practice of defining routes within routes, allowing for hierarchical page structures and dynamic URLs. This approach is commonly used to create complex and nested page layouts.

To demonstrate nested routes, let's consider an example where we have a website for a blog. We want to have a main page displaying a list of blog posts and individual pages for each blog post.

First, we need to set up our routing structure. Next.js uses the file system as the basis for routing. In the project directory, we'll create a "pages" folder and the following files:

1. `pages/index.js`: This will be the main page that lists all the blog posts.
2. `pages/posts.js`: This file will serve as a placeholder for the nested routes related to individual blog posts.
3. `pages/posts/[slug].js`: This file will represent an individual blog post page, where `[slug]` is a dynamic parameter representing the blog post's unique identifier.

Here's an example of how the code for these files might look:

1. `pages/index.js`:
```javascript
// pages/index.js
import React from 'react';

const IndexPage = () => {
  return <div>Welcome to the blog! This is the main page.</div>;
};

export default IndexPage;
```

2. `pages/posts.js`:
```javascript
// pages/posts.js
import React from 'react';

const PostsPage = () => {
  return <div>This is the posts page.</div>;
};

export default PostsPage;
```

3. `pages/posts/[slug].js`:
```javascript
// pages/posts/[slug].js
import React from 'react';
import { useRouter } from 'next/router';

const PostPage = () => {
  const router = useRouter();
  const { slug } = router.query;

  return <div>This is the page for post: {slug}</div>;
};

export default PostPage;
```

With this setup, the URLs will be structured as follows:
- Main page: `http://example.com/`
- Posts page: `http://example.com/posts`
- Individual post page: `http://example.com/posts/[slug]`

For instance, if we have a blog post with the slug "my-first-post," the URL for that post will be `http://example.com/posts/my-first-post`.

Nested routes allow us to define a hierarchy within our pages and create more complex website structures. We can further extend this concept to create additional nested routes by creating more files and folders within the "pages" directory.

Keep in mind that Next.js automatically handles the routing based on the file system structure, so there is no need to set up explicit routing rules.

## Extracting Params from the Dynamic Route

### Client Side

1. **Using the `useRouter` hook**

The `useRouter` hook provides access to the current router state, including the current path and params. To extract the params from the dynamic route, you can use the following code:

```
const { params } = useRouter();
const id = params.id;
```

Here is an example of how to use the `useRouter` hook to extract the params from the dynamic route:

```
import { useRouter } from "next/router";
const Home = () => {
  const { params } = useRouter();

  const id = params.id;

  return (
    <h1>The id is {id}</h1>
  );
};
```

### Server Side

```js
export async function getServerSideProps({ params }) {
    const { productId } = params;
    const response = await fetch(`http://localhost:8080/products/${productId}`);
    const product = await response.json();
    return {
        props: {
            product,
        },
    };  
}
```




