# Database Adapters

Up to this point we can log in to our application via Google. However, in a real application we typically need to store our users in a database. This is where the use of adapters comes in. If we use an adapter, when someone logs in, Auth.js automatically stores their data in a database.

To get started, install the prisma-adapter using the following command:

```Bash
npm i @auth/prisma-adapter
```

Next specify the adapter as part of initializing Auth.js in the `auth.ts` file.

**/auth.ts:**

```TS
import NextAuth from "next-auth";
import GoogleProvider from "next-auth/providers/google";
import { PrismaAdapter } from "@auth/prisma-adapter";
import prisma from "./prisma/client";

export const { auth, handlers, signIn, signOut } = NextAuth({
  adapter: PrismaAdapter(prisma),
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
});

```

Finally, replace existing models in your schema.prisma file with the following models:

```scheme
model Account {
  id                 String  @id @default(cuid())
  userId             String  @map("user_id")
  type               String
  provider           String
  providerAccountId  String  @map("provider_account_id")
  refresh_token      String? @db.Text
  access_token       String? @db.Text
  expires_at         Int?
  token_type         String?
  scope              String?
  id_token           String? @db.Text
  session_state      String?
 
  user User @relation(fields: [userId], references: [id], onDelete: Cascade)
 
  @@unique([provider, providerAccountId])
  @@map("accounts")
}
 
model Session {
  id           String   @id @default(cuid())
  sessionToken String   @unique @map("session_token")
  userId       String   @map("user_id")
  expires      DateTime
  user         User     @relation(fields: [userId], references: [id], onDelete: Cascade)
 
  @@map("sessions")
}
 
model User {
  id            String    @id @default(cuid())
  name          String?
  email         String?   @unique
  emailVerified DateTime? @map("email_verified")
  image         String?
  accounts      Account[]
  sessions      Session[]
 
  @@map("users")
}
 
model VerificationToken {
  identifier String
  token      String
  expires    DateTime
 
  @@unique([identifier, token])
  @@map("verification_tokens")
}
```

The above models facilitate storing of sessions in a database rather than using jwt (json web tokens).