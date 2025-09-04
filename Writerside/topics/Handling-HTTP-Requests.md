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