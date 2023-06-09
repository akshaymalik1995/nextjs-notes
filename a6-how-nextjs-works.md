# How nextjs works?

Before you learn more advanced Next.js features, it would be helpful to understand the basics of how Next.js works.

In the next sections, we’ll look at what happens to your application code during these different stages:

* The environment where your code runs: **Development vs. Production**
* When your code runs: **Build Time vs. Runtime**
* Where rendering happens: **Client vs. Server**

Now let’s dive deeper into these concepts and discuss some of the processes Next.js is doing behind the scenes.

## Development and Production Environments

You can think of environments as the context in which your code is running.

During development, you’re building and running the application on your local machine. Going to production is the process of making your application ready to be deployed and consumed by users.

### How this applies to Next.js
Next.js provides features for both the development and production stages of an application. For example:

* In the development stage, Next.js optimizes for the developer and their experience building the application. It comes with features that aim to improve the Developer Experience such the TypeScript and ESLint integration, Fast Refresh, and more.
* In the production stage, Next.js optimizes for the end-users, and their experience using the application. It aims to transform the code to make it performant and accessible.

Since each environment has different considerations and goals, there is a lot that needs to be done to move an application from development to production. For instance, the application code needs to be compiled, bundled, minified, and code split.

### The Next.js Compiler
Next.js handles much of these code transformations and underlying infrastructure to make it easier for your application to go to production.

This is made possible because Next.js has a compiler written in Rust, a low-level programming language, and SWC, a platform that can be used for compilation, minification, bundling, and more.

In the next sections, we'll explore what each of these transformations are.

## What is Compiling?
Developers write code in languages that are more developer-friendly such as JSX, TypeScript, and modern versions of JavaScript. While these languages improve the efficiency and confidence of developers, they need to be compiled into JavaScript before browsers can understand them.

Compiling refers to the process of taking code in one language and outputting it in another language or another version of that language.

![image](https://github.com/akshaymalik1995/nextjs-notes/assets/55041489/adb2f60e-c67c-423a-9432-c27b8c90a29e)

In Next.js, compilation happens during the development stage as you edit your code, and as part of the build step to prepare your application for production.

## What is Minifying?

Developers write code that is optimized for human readability. This code might contain extra information that is not necessary for the code to run, such as comments, spaces, indents, and multiple lines.

![image](https://github.com/akshaymalik1995/nextjs-notes/assets/55041489/b84e180b-931e-4102-b724-c35f6dd4e49c)

Minification is the process of removing unnecessary code formatting and comments without changing the code’s functionality. The goal is to improve the application’s performance by decreasing file sizes.

In Next.js, JavaScript and CSS files are automatically minified for production.

## What is Bundling?

Developers break up their application into modules, components, and functions that can be used to build larger pieces of their application. Exporting and importing these internal modules, as well as external third-party packages, creates a complex web of file dependencies.

![image](https://github.com/akshaymalik1995/nextjs-notes/assets/55041489/3ff2ce6c-c847-4952-8df7-eaf15fa170f1)

Bundling is the process of resolving the web of dependencies and merging (or ‘packaging’) the files (or modules) into optimized bundles for the browser, with the goal of reducing the number of requests for files when a user visits a web page.


## What is Code Splitting?
Developers usually split their applications into multiple pages that can be accessed from different URLs. Each of these pages becomes a unique entry point into the application.

Code-splitting is the process of splitting the application’s bundle into smaller chunks required by each entry point. The goal is to improve the application's initial load time by only loading the code required to run that page.


![image](https://github.com/akshaymalik1995/nextjs-notes/assets/55041489/91c15c43-5376-4b65-8b0a-8895f9a1a667)

Next.js has built-in support for code splitting. Each file inside your pages/ directory will be automatically code split into its own JavaScript bundle during the build step.

Further:

* Any code shared between pages is also split into another bundle to avoid re-downloading the same code on further navigation.
* After the initial page load, Next.js can start pre-loading the code of other pages users are likely to navigate to.
* Dynamic imports are another way to manually split what code is initially loaded.

## Build Time and Runtime

**Build time** (or build step) is the name given to a series of steps that prepare your application code for production.

When you build your application, Next.js will transform your code into production-optimized files ready to be deployed to servers and consumed by users. These files include:

* HTML files for statically generated pages
* JavaScript code for rendering pages on the server
* JavaScript code for making pages interactive on the client
* CSS files

**Runtime** (or request time) refers to the period of time when your application runs in response to a user’s request, after your application has been built and deployed.


## Client and Server

In the context of web applications, the client refers to the browser on a user’s device that sends a request to a server for your application code. It then turns the response it receives from the server into an interface the user can interact with.

![image](https://github.com/akshaymalik1995/nextjs-notes/assets/55041489/d8eb4aae-bb3f-464c-92b8-b1183c52d6cb)

Server refers to the computer in a data center that stores your application code, receives requests from a client, does some computation, and sends back an appropriate response.

## What is rendering?

There is an unavoidable unit of work to convert the code you write in React into the HTML representation of your UI. This process is called **rendering**.

Rendering can take place on the server or on the client. It can happen either ahead of time at build time, or on every request at runtime.

With Next.js, three types of rendering methods are available: **Server-Side Rendering**, **Static Site Generation**, and **Client-Side Rendering**.

### Pre-Rendering

Server-Side Rendering and Static Site Generation are also referred to as **Pre-Rendering** because the fetching of external data and transformation of React components into HTML happens before the result is sent to the client.

### Client-Side Rendering vs. Pre-Rendering
In a standard React application, the browser receives an empty HTML shell from the server along with the JavaScript instructions to construct the UI. This is called **client-side rendering** because the initial rendering work happens on the user's device.

![image](https://github.com/akshaymalik1995/nextjs-notes/assets/55041489/c91f3f6a-e428-4c86-8480-0590a1af8d05)

> **Note:** You can opt to use client-side rendering for specific components in your Next.js application by choosing to fetch data with React’s `useEffect()` or a data fetching hook such as `useSWR`.

In contrast, Next.js **pre-renders** every page by default. Pre-rendering means the HTML is generated in advance, on a server, instead of having it all done by JavaScript on the user's device.
       
In practice, this means that for a fully client-side rendered app, the user will see a blank page while the rendering work is being done. Compared to a pre-rendered app, where the user will see the constructed HTML:

![image](https://github.com/akshaymalik1995/nextjs-notes/assets/55041489/6c34668a-0b31-4512-bfa0-e877ffd2d2b6)

Let’s discuss the two types of pre-rendering:

### Server-Side Rendering

With server-side rendering, the HTML of the page is generated on a server for each request. The generated HTML, JSON data, and JavaScript instructions to make the page interactive are then sent to the client.

On the client, the HTML is used to show a fast non-interactive page, while React uses the JSON data and JavaScript instructions to make components interactive (for example, attaching event handlers to a button). This process is called hydration.

In Next.js, you can opt to server-side render pages by using **getServerSideProps**.

### Static Site Generation

With Static Site Generation, the HTML is generated on the server, but unlike server-side rendering, there is no server at runtime. Instead, content is generated once, at build time, when the application is deployed, and the HTML is stored in a CDN and re-used for each request.

In Next.js, you can opt to statically generate pages by using **getStaticProps**.

> **Note:** You can use Incremental Static Regeneration to create or update static pages after you’ve built your site. This means you do not have to rebuild your entire site if your data changes.

The beauty of Next.js is that you can choose the most appropriate rendering method for your use case on a page-by-page basis, whether that's Static Site Generation, Server-side Rendering, or Client-Side Rendering. 

In the next section, we’ll discuss where your code can be stored or run after it’s deployed.

## What is the network?

It’s helpful to know where your application code is stored and run once it’s deployed to the network. You can think of the network as linked computers (or servers) capable of sharing resources. In the case of a Next.js application, your application code can be distributed to **origin servers**, **Content Delivery Networks (CDNs)**, and **the Edge**. Let’s see what each of these are:

### Origin Servers
As we discussed earlier, the server refers to the main computer that stores and runs the original version of your application code.

We use the term origin to distinguish this server from the other places application code can be distributed to, such as **CDN servers** and **Edge servers**.

When an origin server receives a request, it does some computation before sending a response. The result of this computation work can be moved to a CDN (Content Delivery Network).

### Content Delivery Network

CDNs store static content (such as HTML and image files) in multiple locations around the world and are placed between the client and the origin server. When a new request comes in, the closest CDN location to the user can respond with the cached result.

![image](https://github.com/akshaymalik1995/nextjs-notes/assets/55041489/855d02ed-85ac-433f-9810-1f8c2510106f)

This reduces the load on the origin because the computation doesn’t have to happen on each request. It also makes it faster for the user because the response comes from a location geographically closer to them.

In Next.js, since pre-rendering can be done ahead of time, CDNs are well suited to store the static result of the work - making content delivery faster.

### The Edge
The Edge is a generalized concept for the fringe (or edge) of the network, closest to the user. CDNs could be considered part of "the Edge" because they store static content at the fringe (edge) of the network.

Similar to CDNs, Edge servers are distributed to multiple locations around the world. But unlike CDNs, which store static content, some Edge servers can run small snippets of code.

This means both **caching** and **code execution** can be done at the Edge closer to the user.

By moving some work that was traditionally done client-side or server-side to the Edge, you can make your application more performant because it reduces the amount of code sent to the client, and part of the user's request does not have to go all the way back to the origin server - thus reducing latency.

In Next.js, you can run code at the Edge with Middleware, and soon with React Server Components.

