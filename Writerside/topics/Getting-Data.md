# Getting Data

You need to import the prisma client first to get data from the database.

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