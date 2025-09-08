# Validating Requests with Zod

For the code below an if statement is used to validate the user object sent with the request.

**app/api/user/[id]/route.tsx:**

```TSX
import { NextRequest, NextResponse } from "next/server";

export async function PUT (request: NextRequest, {params}: {params: {id: number}}) {
    const body = await request.json();

    if (!body.name) {
        return NextResponse.json({error: 'Name is required'}, {status: 400})
    }

    if (params.id > 10) {
        return NextResponse.json({error: "User not found."}, {status: 404})
    }

    return NextResponse.json({id: 1, name: body.name})
}
```

This works for simple objects but for more complex objects we'll end up with too many if-statements thus making it better to use a validation library like **Zod**.

To get started, install Zod in the terminal using the following command:

```bash
npm i zod
```

Next add a schema.tsx file in the **app/api/users** directory where you'll define the shape of the user object.

**app/api/users/schema.tsx:**

```TSX
import z from "zod";

const schema = z.object({
    name: z.string().min(3),
})

export default schema;
```

In the route file, import schema and call the safeParse method instead of using the if-statement to perform validation.

**app/api/user/[id]/route.tsx:**

```TSX
import { NextRequest, NextResponse } from "next/server";
import schema from "../schema";

export async function PUT(
  request: NextRequest,
  { params }: { params: { id: number } }
) {
  const body = await request.json();
  
  const validation = schema.safeParse(body);
  if (!validation.success) {
    return NextResponse.json(validation.error.errors, { status: 400 });
  }

  if (params.id > 10) {
    return NextResponse.json({ error: "User not found." }, { status: 400 });
  }

  return NextResponse.json({ id: 1, name: body.name });
}
```

The same can also be done for the POST function:

**app/api/users/route.tsx:**

```TSX
import { NextRequest, NextResponse } from "next/server";
import schema from "./schema";

export function GET(request: NextRequest) {
    return NextResponse.json([
        {id: 1, name: "Levis"},
        {id: 2, name: "John"},
    ])
}

export async function POST(request: NextRequest) {
   const body = await request.json(); 
   const validation = schema.safeParse(body);

   if(!validation.success) {
    return NextResponse.json(validation.error.errors, {status: 400})
   }
   return NextResponse.json(body);
}
```