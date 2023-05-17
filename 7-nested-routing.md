# Nested Routes

Nested routes in Next.js are routes that are defined within other routes. For example, you could have a route at `/products` and then nested routes at `/products/apple` and `/products/banana`.

To create nested routes, you can nest folders inside each other in the `pages` directory. For example, you could create a folder named `products` inside the `pages` directory and then create two files inside the `products` folder, one named `index.js` and one named `apple.js`.

The `index.js` file would be the main page for the `/products` route and the `apple.js` file would be the main page for the `/products/apple` route.

You can access nested routes by navigating to the corresponding URL in your browser. For example, you could navigate to `/products` to see the main page for the `/products` route and you could navigate to `/products/apple` to see the main page for the `/products/apple` route.

Here is an example of how to create nested routes in Next.js:

```
pages
  products
    index.js
    apple.js
```

The `index.js` file would contain the following code:

```js
export default function Products() {
  return (
    <div>
      <h1>Products</h1>
      <ul>
        <li><a href="/products/apple">Apple</a></li>
        <li><a href="/products/banana">Banana</a></li>
      </ul>
    </div>
  );
}
```

The `apple.js` file would contain the following code:

```js
export default function Apple() {
  return (
    <div>
      <h1>Apple</h1>
    </div>
  );
}
```

Nested routes can be a useful way to organize your application and to make it easier for users to find the information they are looking for.
