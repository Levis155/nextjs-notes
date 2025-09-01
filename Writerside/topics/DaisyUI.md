# DaisyUI

DaisyUI is the most popular component library for Tailwind CSS. It adds component class names to Tailwind CSS.

## Installation and Setup

To get started, install daisyUI as a development dependency with the following command:

```shell
npm i -D daisyui
```

Then add daisyUI to your **tailwind.config.js** file:

```js
module.exports = {
    /...
    plugins: [require("daisyui")],
}
```

## Components and Features

### Components

DaisyUI comes with 50+ components, e.g. Accordion, Alerts, Carousel, Buttons,Chat bubble, Cards e.t.c

The button component for instance has predefined classes similar to bootstrap i.e. **btn, btn-neutral, btn-primary, btn-secondary, btn-accent, e.t.c** These classes use tailwind under the hood and removes the necessity of manually combining a bunch of small tailwind classes to create a button. 

Example:

```tsx
<button className="btn btn-primary">add to cart</button>
```


```TSX
interface User {
  id: number;
  name: string;
  email: string;
}

const UsersPage = async () => {
  const res = await fetch(`https://jsonplaceholder.typicode.com/users`, {
    cache: "no-store",
  });
  const users: User[] = await res.json();

  return (
    <>
      <h1>Users</h1>
      <table className="table table-bordered">
        <thead>
          <tr>
            <th>Name</th>
            <th>Email</th>
          </tr>
        </thead>

        <tbody>
          {users.map((user) => (
            <tr key={user.id}>
              <td>{user.name}</td>
              <td>{user.email}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </>
  );
};

export default UsersPage;

```

### Themes

daisyUI comes with a number of themes which can be used with no extra effort. Each theme defines a set of colors which will be used on all daisyUI elements.

To use a theme, add its name in **tailwind.config.js** and activate it by adding data-theme attribute to `HTML` tag:

**tailwind.config.ts:**
```TSX
module.exports = {
    //...
    daisyui: {
        themes: ["light", "dark", "cupcake"],
    },
}
```

**layout.tsx:**
```tsx
<html data-theme="cupcake"></html>
```