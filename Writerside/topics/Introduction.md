# Introduction

Next.js is a powerful framework for building fast and search-engine friendly applications.

It is built on top of React.js and while react.js is just a library for creating interactive user interfaces, next.js is a comprehensive framework. It includes its own **routing library, a compiler for transforming and minifying JavaScript code, a CLI for building and starting applications, and Node.js runtime.**

**What is a Node.js runtime?** There are basically two ways we can execute Javascript code: within a web browser on the client side or within a Node.js Runtime on the server side. Thus, a Node.js runtime is just a fancy term for a program that can execute javascript code.

Next.js having a Node.js runtime allows us to achieve the following:

- **Full-stack Development:** We can write both the front-end and backend-code within the same Next.js project. (backend code is executed within a Node.js runtime and frontend code is bundled and sent to the client for execution within a web browser )
- **Server-side Rendering:** We can render components on the server and send their content to the client. This improves the speed and search-friendliness of applications.
- **Static Site Generation:** We can pre-render certain pages or components that have static data when we build our applications. We just render them once and serve them whenever they are needed.