# Dynamic Routes

A dynamic route is a route with a parameter.

For instance, we can have a users route with an id parameter:

```bash
app/
 └── page.tsx      →  "/"
 └── users/
       └── page.tsx      →  "/users"
       └── new/
            └── page.tsx      →  "/users/new"
       └── [id]/
            └── page.tsx      →  "/users/id"

```

Assuming page.tsx in `[id]/` returns a component **UserDetailPage**, to access our route parameter, we need to pass props to the component:

**app/users/[id]/page.tsx:**

```tsx
import React from 'react'

interface Props {
    params: {id: number}
}

const UserDetailPage = ({params: {id}}: Props) => {
  return (
    <div>
      UserDetailPage {id}
    </div>
  )
}

export default UserDetailPage

```

<note>The above approach only works in pages. We can not add `Props` to a component that is used on this page. If on this page we have a component that needs to know the user id we have to grab the user id at the page level and then pass it as a prop to the component.</note>