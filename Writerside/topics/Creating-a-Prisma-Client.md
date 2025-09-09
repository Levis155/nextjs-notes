# Creating a Prisma Client

To work with our database first we'll need to create a Prisma Client.

To get started, in the prisma folder add a `client.ts` file.

**client.ts:**

```ts
import { PrismaClient } from "@/app/generated/prisma";

const prisma = new PrismaClient();

export default prisma;
```

> In Next.js due to fast refresh, any time we change our source code, Next.js refreshes some of our modules. In this case we'll end up in a situation where we have too many prisma clients. To go around this we have to modify client.ts as follows.

```ts
import { PrismaClient } from "@/app/generated/prisma";

declare global {
  var prisma: PrismaClient | undefined;
}

let prisma: PrismaClient;

if (process.env.NODE_ENV === "production") {
  prisma = new PrismaClient();
} else {
  if (!global.prisma) {
    global.prisma = new PrismaClient();
  }
  prisma = global.prisma;
}

export default prisma;
```