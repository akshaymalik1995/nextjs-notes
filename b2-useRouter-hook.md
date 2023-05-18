# The useRouter Hook

The `useRouter` hook is a React hook that provides access to the current router state. It can be used to get information about the current route, such as the path, query parameters, and hash. It can also be used to navigate to new routes.

To use the `useRouter` hook, you need to import it from the `next/router` package. Then, you can use it in any component that you want to access the router state.

The `useRouter` hook returns an object with the following properties:

* `pathname`: The path of the current route.
* `query`: The query parameters of the current route.
* `hash`: The hash of the current route.
* `asPath`: The URL of the current route, including the query parameters and hash.
* `isFallback`: A boolean value that indicates whether the current route is a fallback route.
* `match`: An object that contains information about the current route match.
* `history`: An object that provides methods for navigating to new routes.

Here is an example of how to use the `useRouter` hook to get the path of the current route:

```
import React, { useRouter } from 'react';

export default function Home() {
  const router = useRouter();
  const path = router.pathname;

  return (
    <h1>The current path is {path}</h1>
  );
}
```

This code will render the text "The current path is /" if the user is on the home page. If the user is on a different page, the text will be updated to reflect the current path.

The `useRouter` hook can also be used to navigate to new routes. To do this, you can use the `push` method on the `history` object. The `push` method takes a path as its argument, and it will navigate the browser to the specified path.

Here is an example of how to use the `useRouter` hook to navigate to the `/about` page:

```
import React, { useRouter } from 'react';

export default function Home() {
  const router = useRouter();

  function handleClick() {
    router.history.push('/about');
  }

  return (
    <div>
      <h1>The current path is {router.pathname}</h1>
      <button onClick={handleClick}>Go to About</button>
    </div>
  );
}
```

This code will render the text "The current path is /" if the user is on the home page. If the user clicks on the "Go to About" button, the browser will navigate to the `/about` page.

The `useRouter` hook is a powerful tool that can be used to access the current router state and navigate to new routes. It can be used in any component that you want to access the router state.
