# Handling Not Found Errors

In Next.js projects we get a default 404 page when we go to a page that doesn't exist, but we can always customize it.

We can add a special file named **not-found** in the app folder that Next.js router looks for.

**app/not-found.tsx:**

```TSX
import React from 'react'

const NotFoundPage = () => {
  return (
    <div>
      The requested page doesn't exist.
    </div>
  )
}

export default NotFoundPage

```

We can also create custom not-found pages for different parts of our application. For instance if we try to look at a user that doesn't exist from a users page we want to show a custom not-found page with the message the given user does not exist.

**app/users/[id]/page.tsx:**

```TSX
import { notFound } from 'next/navigation'
import React from 'react'

interface Props {
    params: {id: number}
}

const UserDetailPage = ({params: {id}}: Props) => {
  if(id > 10) notFound();
  return (
    <div>
      UserDetailPage {id}
    </div>
  )
}

export default UserDetailPage

```

**app/users/[id]/not-found.tsx:**

```TSX
import React from 'react'

const UserNotFoundPage = () => {
  return (
    <div>
      This user doesn't exist.
    </div>
  )
}

export default UserNotFoundPage

```