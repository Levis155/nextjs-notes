# Creating Data

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