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
