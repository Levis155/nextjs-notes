# Routing and Navigation

## Routing in Next.js

Routing means deciding which page (or component) to show when a user visits a certain URL in your app.

Example:

- Visiting / → shows homepage 
- Visiting /about → shows about page 
- Visiting /contact → shows contact page

In Next.js, routing is file-based → the folder structure in your app/ directory determines your routes.

Every folder you create in the app/ directory with a page.tsx, page.jsx or page.js file becomes a route automatically.

**Example**

```bash
app/
 └── page.tsx      →  "/"
 └── users/
       └── page.tsx      →  "/users"

```

You can implement a nested route under /users for instance /users/new to display new users by adding a folder "new" to the users directory with a page.tsx file.

```bash
app/
 └── page.tsx      →  "/"
 └── users/
       └── page.tsx      →  "/users"
       └── new/
            └── page.tsx      →  "/users/new"

```

## Navigation Between Pages

To move between pages, you use the Link component from next/link.

```jsx
import Link from 'next/link';

export default function Home() {
  return (
    <div>
      <h1>Homepage</h1>
      <Link href="/users">Go to Users Page</Link>
    </div>
  );
}

```

Unlike a normal `<a>` tag, `<Link>` makes navigation faster because Next.js preloads pages in the background.