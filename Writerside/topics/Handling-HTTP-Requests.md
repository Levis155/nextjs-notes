# Handling HTTP Requests

## Getting a collection of Objects
To handle http requests a route file is created. For instance http requests for multiple users' data can be handled within the `app/api/users/route.tsx` file.

**app/api/users/route.tsx:**

```TSX
import { NextRequest, NextResponse } from "next/server";

export function GET(request: NextRequest) {
    return NextResponse.json([
        {id: 1, name: "Levis"},
        {id: 2, name: "John"},
    ])
}
```

> In a given folder or URL segment you can either have a page file or a route file but not both.

In the route file we can create one or more route handlers. A route handler is a function that handles http requests i.e. **GET, POST, PUT** e.t.c.

## Getting a Single Object

To create an api endpoint for getting a single object e.g. a single user's details a requirement would be to pass the id of the object (user) in the URL e.g. `localhost:3000/api/users/1`

This can be implemented as follows:

```TSX
import { NextRequest, NextResponse } from "next/server";

export function GET(
  request: NextRequest,
  { params }: { params: { id: number } }
) {
  if (params.id > 10)
    return NextResponse.json({ error: "User not found" }, { status: 404 });

  return NextResponse.json({ id: 1, name: "Levis" });
}

```

For demonstration purposes, the above function returns a status of 404 if the id is more than 10 and returns a user object if the id is not.

## Creating an Object

To create an object i.e. a user object, we send a request to the user's endpoint and include the user object in the body of the request.

**app/api/users/route.tsx:**

```TSX
import { NextRequest, NextResponse } from "next/server";
 
 export async function POST(request: NextRequest) {
   const body = await request.json(); 
   return NextResponse.json(body);
}

```

The above function returns the object we've sent to the server.

## Updating an Object

To update a user we should send a request to an endpoint representing an individual user e.g. `localhost:300/api/users/1` including the user object in the body of the request.

We can use PUT or PATCH functions for updating an object but technically speaking we should use PUT for replacing an object and PATCH for updating one or more properties.

**app/api/users/[id]/route.tsx:**

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

The above function simulates how object updates are handled in real-world scenarios when interacting with databases. i.e.
- Validate request body
- If invalid return 400
- Fetch the user with the given id
- If doesn't exist, return 404
- Update the user
- Return the updated user

## Deleting an Object

When deleting an object we need the parameters passed in the PUT function too.

**app/api/users/[id]/route.tsx:**

```TSX
import { NextRequest, NextResponse } from "next/server";

export function DELETE(
  request: NextRequest,
  { params }: { params: { id: number } }
) {
  if (params.id > 10) {
    return NextResponse.json({ error: "User not found" }, { status: 404 });
  }

  return NextResponse.json({});
}
```

The above delete function simulates the following scenario:
- Fetch the user from the db
- If not found, return 404
- Delete the user
- Return 200