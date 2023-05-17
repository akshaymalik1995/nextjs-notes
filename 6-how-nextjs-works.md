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


