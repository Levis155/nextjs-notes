# Static and Dynamic Rendering

## Static rendering

In Next.js we have another performance-optimization technique called **static rendering** or **static-side generation**

The idea behind static rendering is that if we have pages or components that have static data, we can have Next.js render them once when we build our application for production (Next.js is not going to re-render them rather it's going to get their payload or content from it's cache which is based on the file system).

## Dynamic rendering

In comparison, this rendering happens at request time.

To demonstrate dynamic rendering in action we can include a time-stamp to the following users page:

```tsx
interface User {
    id: number;
    name: string;
}

const UsersPage = async () => {
    const res = await fetch(`https://jsonplaceholder.typicode.com/users`);
    const users: User[] = await res.json();

    return (
        <>
            <p>{new Date().toLocaleTimeString()}</p>
            <h1>Users</h1>
            <ul>
                {users.map(user => <li key={user.id}>{user.name}</li>)}
            </ul>
        </>
    )
}

export default UsersPage;
```

Upon refreshing the time stamp keeps changing. This however only happens in development mode. If we build this application for production, the timestamp does not change because next.js treats the page as a static page. 

Why is this so? **By default whenever the `fetch()` function is used, next.js caches the data thus it treats it as static or unchanging data. Thus when rendering this page, Next.js renders it statically at build time due to the presence of static data.**

Disabling caching as shown below enforces Next.js to render the page at request time or dynamically.

```TSX
    const res = await fetch(`https://jsonplaceholder.typicode.com/users`, {cache: 'no-store'});
```