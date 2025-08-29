# Data Fetching

Data is typically fetched through two ways:
- On the client
- On the server

## Data Fetching on the Client

To fetch data on the client we typically use the `useState()` hook to declare a state variable and the `useEffect()` hook to call the backend, get the data and put it in our state variable.

React Query is however a better alternative to manually using the state and effect hooks.

Fetching data on the client in client components has all the problems discussed with client side components. i.e.
- Large bundles
- Resource intensiveness
- No SEO
- Less secure
- Extra roundtrip to server. (extra problem) Whenever a react application loads first the browser downloads the html template as well as the css and JavaScript files from the backend then it will send an extra request to fetch data from the backend.

**Fetching data in our server components gets rid of all these problems.**

## Data Fetching on the Server

The beauty of data fetching in server components is that Server Components are default, so you can fetch data directly with `fetch()` at the top of a component. 

**Example:**

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
            <h1>Users</h1>
            <ul>
                {users.map(user => <li key={user.id}>{user.name}</li>)}
            </ul>
        </>
    )
}

export default UsersPage;
```