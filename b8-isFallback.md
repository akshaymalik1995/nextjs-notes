# How to use the `isFallback` property in Next.js to display a loading skeleton while a dynamic page is being generated

When you're building a Next.js application, you may have dynamic pages that are generated at runtime based on user input or data from an API. These pages can take some time to generate, especially if they require a lot of data or complex calculations. During this time, the user may see a blank page or a loading spinner, which can be frustrating and lead to a poor user experience.

To improve the user experience, you can use the `isFallback` property in Next.js to display a loading skeleton while the dynamic page is being generated. The `isFallback` property is a boolean value that is set to `true` when a dynamic page is being generated, and `false` when the page has been generated.

Here's an example of how you can use the `isFallback` property to display a loading skeleton:

```javascript
import { useRouter } from 'next/router';
import LoadingSkeleton from '../components/LoadingSkeleton';

export default function Product({ product }) {
  const router = useRouter();

  if (router.isFallback) {
    return (
      <main className="flex flex-col space-y-10 justify-center items-center ">
        <LoadingSkeleton />
        <button onClick={goBack} className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
          Back to products
        </button>
      </main>
    );
  }

  return (
    <div>
      <h1>{product.title}</h1>
      <p>{product.description}</p>
      <img src={product.image} alt={product.title} />
    </div>
  );
}
```

In this code, we're importing the `useRouter` hook from the `next/router` module, which allows us to access the router object and check the `isFallback` property.

Inside the `Product` component, we're checking if `router.isFallback` is `true`. If it is, we're returning a loading skeleton component and a button to go back to the products page. The loading skeleton component can be any component that you want to display while the page is being generated, such as a spinner or a placeholder image.

If `router.isFallback` is `false`, we're rendering the product details, such as the title, description, and image.

By using the `isFallback` property in this way, you can improve the user experience of your Next.js application by displaying a loading skeleton while dynamic pages are being generated. This can help to reduce frustration and improve engagement with your application.
