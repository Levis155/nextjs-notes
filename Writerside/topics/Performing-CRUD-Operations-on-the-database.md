# Performing CRUD Operations on the database

You need to import the prisma client first to manipulate data from the database.

## Getting all users

**app/api/users/route.tsx:**

```TSX
import { NextRequest, NextResponse } from "next/server";
import prisma from "@/prisma/client";

export async function GET(request: NextRequest) {
    const users = await prisma.user.findMany();

    return NextResponse.json(users, {status: 200})
}
```

## Getting a Single User

**app/api/users/[id]/route.tsx:**

```TSX
import { NextRequest, NextResponse } from "next/server";
import prisma from "@/prisma/client";

export async function GET(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const user = await prisma.user.findUnique({
    where: {id: parseInt(params.id)}
  });
  
  if (!user)
    return NextResponse.json({ error: "User not found" }, { status: 404 });

  return NextResponse.json(user);
}
```

## Creating a User

```tsx
import { NextRequest, NextResponse } from "next/server";
import schema from "./schema";
import prisma from "@/prisma/client";

export async function POST(request: NextRequest) {
   const body = await request.json(); 
   const validation = schema.safeParse(body);

   if(!validation.success) {
    return NextResponse.json(validation.error, {status: 400})
   }

   const user = await prisma.user.findUnique({
    where: {email: body.email}
   })

   if (user) {
    return NextResponse.json({error: 'User already exists'}, {status: 400})
   }

   const newUser = await prisma.user.create({
    data: {
        name: body.name,
        email: body.email,
    }
   })
   return NextResponse.json(newUser, {status: 201});
}
```

> Due to the unique constraint given to the email property we need to first verify if the email is already in use and handle the error accordingly.

## Updating a User

```TSX
import { NextRequest, NextResponse } from "next/server";
import schema from "./schema";
import prisma from "@/prisma/client";

export async function PUT(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const body = await request.json();

  const validation = schema.safeParse(body);
  if (!validation.success) {
    return NextResponse.json(validation.error, { status: 400 });
  }

  const user = await prisma.user.findUnique({
    where: { id: parseInt(params.id) },
  });

  if (!user) {
    return NextResponse.json({ error: "User not found." }, { status: 400 });
  }

  const updatedUser = await prisma.user.update({
    where: { id: user.id },
    data: {
      name: body.name,
      email: body.email,
    }
  })
  return NextResponse.json(updatedUser, {status: 200});
}
```

## Deleting a User

```TSX
import { NextRequest, NextResponse } from "next/server";
import schema from "./schema";
import prisma from "@/prisma/client";

export async function DELETE(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const user = await prisma.user.findUnique({
    where: { id: parseInt(params.id) },
  });

  if (!user) {
    return NextResponse.json({ error: "User not found" }, { status: 404 });
  }

  await prisma.user.delete({
    where: { id: user.id },
  });

  return NextResponse.json({});
}
```