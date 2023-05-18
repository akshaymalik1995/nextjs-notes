# The `_app.js` file
```jsx

import Layout from './layout'

// App component to render the current page
export default function App(props) {
  // This `Component` is the current page
  // This `pageProps` is the props of the current page
  const { Component, pageProps } = props;
  const noLayout = Component.noLayout || false;
  if (noLayout) { 
    return <Component {...pageProps} />
  }
  
  return (
    <Layout>
      {/* Rendering the current page */}
      <Component {...pageProps} />
    </Layout>
  );
}
```

The `App` component render the component that is required to display the current page that the client has accessed.

As a prop, it recieves the component that needs to be rendered to display UI for the current page and also the props required for that component.
