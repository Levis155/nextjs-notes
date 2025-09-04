# Getting a Collection of Objects

To handle http requests a route file is created. For instance http requests for users' data can be handled within the `app/api/users/route.tsx` file.

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