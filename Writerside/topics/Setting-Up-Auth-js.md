# Setting Up Auth.js

Auth.js is a library that helps developers add authentication (login, signup, and session handling) to their web apps easily.

It’s mainly used in Next.js (a React framework), but it can also work with other JavaScript/TypeScript backends.

Instead of writing all the code to manage login, tokens, sessions, and third-party providers (like Google, GitHub, or Facebook logins), Auth.js gives you ready-made tools.

## Installation

Install Auth.js into your project by running the following command:

```Bash
npm install next-auth@beta
```

## Adding Route handlers

Auth.js actually uses route handlers for its authentication endpoints. For example, you set up an `/api/auth/[...nextauth]/route.ts` file, and Auth.js puts all the login/logout/session logic there.

In this file you have to create a handler function by importing and calling NextAuth. We pass a configuration object to NextAuth which we'll come back to.

We then export the handler function with 2 different names i.e. GET and POST. This means any GET and POST request sent to this endpoint will be handled inside the handler function.

```TS
import NextAuth from "next-auth";

const handler = NextAuth({})

export { handler as GET, handler as POST}
```

## Creating .env Variables

Finally, we need to create environment variables for `NEXTAUTH_URL` and set it to the address of our website and `NEXTAUTH_SECRET` which has to be a long random string which Auth.js will use to encrypt and sign the authentication keys.

> To generate a long random string you can run the following command in the node terminal: `require('crypto').randomBytes(32).toString('hex')`
