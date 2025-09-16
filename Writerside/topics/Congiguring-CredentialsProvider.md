# Configuring CredentialsProvider

Social logins are great but what if we want to allow users to log in with their usernames and passwords? Well we can certainly do this but a fair amount of work is required to achieve this. i.e. Storing passwords in an encrypted format, implementing functionalities for users to register, change their password e.t.c.

To get started with implementing this, in the `auth.ts` configuration file, you need to import the Credentials Provider from `next-auth/providers/credentials` and pass it in the array of providers. You need to then pass an object within the credentials provider with a credentials field which generates a form in the sign-in page. In addition to that you need to implement the authorize function where you validate the user and make sure they pass the correct username and password combination.

**./auth.ts:**

```TypeScript
import NextAuth from "next-auth";
import GoogleProvider from "next-auth/providers/google";
import Credentials from "next-auth/providers/credentials";
import { PrismaAdapter } from "@auth/prisma-adapter";
import prisma from "./prisma/client";
import bcrypt from 'bcrypt';

export const { auth, handlers, signIn, signOut } = NextAuth({
  adapter: PrismaAdapter(prisma),
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
    Credentials({
      credentials: {
        email: { label: "Email", type: "text", placeholder: "Email" },
        password: { label: "Password", type: "password", placeholder: "Password" },
      },
      async authorize(credentials, req) {
        if (!credentials?.email || !credentials?.password) {
          return null;
        }

        const user = await prisma.user.findUnique({
          where: { email: credentials.email as string}
        })

        if (!user) return null;

        const passwordsMatch = await bcrypt.compare(credentials.password as string, user.hashedPassword as string);

        return passwordsMatch ? user : null;
      },
    }),
  ],
});

```

## Registering Users

To allow users to register, first we have to create an api endpoint. This endpoint will be called by a client component that renders a registration form.

**app/api/register/route.ts**

```TypeScript
import { NextRequest, NextResponse } from "next/server";
import z, { email } from "zod";
import bcrypt from "bcrypt";

const schema = z.object({
  email: z.string(),
  password: z.string().min(5),
});

export async function POST(request: NextRequest) {
  const body = await request.json();

  const validation = schema.safeParse(body);

  if (!validation.success) {
    return NextResponse.json(validation.error, {
      status: 400,
    });
  };

  const user = await prisma?.user.findUnique({
    where: { email: body.email }
  })

  if (user) {
    return NextResponse.json({ error: "User already exists"}, {status: 400})
  }

  const hashedPassword = await bcrypt.hash(body.password, 12);

  const newUser = prisma?.user.create({
    data: {
        email: body.email,
        hashedPassword
    }
  })

  return NextResponse.json({ email: body.email })
}
```