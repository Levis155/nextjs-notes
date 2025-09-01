# Accessing Query String Parameters

Taking an instance of a URL having a query string parameter for determining the sort order of products `/products?sortOrder=name` We can access query string parameters by using the **searchParams** property.

```tsx
import React from 'react'

interface Props {
    params : {slug: string[]};
    searchParams: {sortOrder: string}
}

const ProductPage = ({params: {slug}, searchParams: {sortOrder}}: Props) => {
  return (
    <div>
      ProductPage {slug} {sortOrder}
    </div>
  )
}

export default ProductPage

```

Here is an instance of accessing a query string parameter for determining the sort order for users with help of the fast-sort package:

**app/users/page.tsx:**

```TSX
import UserTable from "./UserTable";

interface Props {
    searchParams: {sortOrder: string}
}

const UsersPage = async ({searchParams: {sortOrder}}: Props) => {
  return (
    <>
      <h1>Users</h1>
      <UserTable sortOrder={sortOrder} />
    </>
  );
};

export default UsersPage;

```

**app/users/UserTable.tsx:**

```TSX
import React from "react";
import Link from "next/link";
import { sort } from "fast-sort";

interface User {
  id: number;
  name: string;
  email: string;
}

interface Props {
  sortOrder: string;
}

const UserTable = async ({ sortOrder }: Props) => {
  const res = await fetch(`https://jsonplaceholder.typicode.com/users`, {
    cache: "no-store",
  });
  const users: User[] = await res.json();

  const sortedUsers = sort(users).asc(
    sortOrder === "email" ? (user) => user.email : (user) => user.name
  );
  return (
    <table className="table table-bordered">
      <thead>
        <tr>
          <th>
            <Link href="/users?sortOrder=name">Name</Link>
          </th>
          <th>
            <Link href="/users?sortOrder=email">Email</Link>
          </th>
        </tr>
      </thead>

      <tbody>
        {sortedUsers.map((user) => (
          <tr key={user.id}>
            <td>{user.name}</td>
            <td>{user.email}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
};

export default UserTable;

```