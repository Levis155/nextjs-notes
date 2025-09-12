# Setting Up Auth.js

Auth.js is a library that helps developers add authentication (login, signup, and session handling) to their web apps easily.

It’s mainly used in Next.js (a React framework), but it can also work with other JavaScript/TypeScript backends.

Instead of writing all the code to manage login, tokens, sessions, and third-party providers (like Google, GitHub, or Facebook logins), Auth.js gives you ready-made tools.

## Installation

Install Auth.js into your project by running the following command:

```Bash
npm install next-auth
```

## Creating the Auth.js Configuration File

Create a configuration file (e.g., `auth.ts` in the project root) that defines your authentication settings. This file will export handlers for API requests and contain the Auth object with configuration options like providers. We'll come back to this object.

**/auth.ts:**

```TS
import NextAuth from "next-auth";
import GoogleProvider from "next-auth/providers/google";

export const { auth, handlers, signIn, signOut } = NextAuth({});

```

## Creating the Auth.js API Route

Create a `app/api/auth/[...nextauth]/route.ts` file to serve as the entry point for authentication API calls by importing and exporting handlers from the main Auth.js configuration file. This catch-all route handler allows Auth.js to manage all related API endpoints under `/api/auth/*`.

**app/api/auth/[...nextauth]/route.ts:**

```TS
import { handlers } from "@/auth";

export const { GET, POST } = handlers;
```

## Creating .env Variables

Finally, we need to create environment variables for `NEXTAUTH_URL` and set it to the address of our website and `NEXTAUTH_SECRET` which has to be a long random string which Auth.js will use to encrypt and sign the authentication keys.

> To generate a long random string you can run the following command in the node terminal: `require('crypto').randomBytes(32).toString('hex')`
