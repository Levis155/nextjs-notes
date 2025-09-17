# Lazy Loading

Lazy loading is a strategy for loading client components or third-party libraries in the future when we need them typically as a result of user-interaction. e.g. button-clicks

## Lazy Loading Client Components

An instance in which we could apply lazy loading could be if we had a heavy component, and we needed to render it as a result of clicking a button as shown below:

**app/components/HeavyComponent.tsx:**

```TSX
import React from 'react'

const HeavyComponent = () => {
  return (
    <div>
      My Heavy Component
    </div>
  )
}

export default HeavyComponent

```

**app/page.tsx:**

```TSX
'use client';

import { useState } from "react";
import HeavyComponent from "./components/HeavyComponent/HeavyComponent";

export default function Home() {
  const [isVisible, setIsVisible] = useState(false)
  return (
    <main>
      <button onClick={() => {setIsVisible(true)}}>Show</button>
      {isVisible && <HeavyComponent />} 
    </main>
  );
}
```

With the above implementation the `HeavyComponent` is still included in our bundle even though we're showing it dynamically. This is because the HeavyComponent is statically imported at the top, so when Next.js builds our application it includes this component in the bundle for our page.

To lazy load this, we have to use the dynamic function from Next.js as shown below:

**app/components/HeavyComponent.tsx:**

```TSX
'use client';

import { useState } from "react";
import dynamic from "next/dynamic";
const HeavyComponent = dynamic(() => import('./components/HeavyComponent/HeavyComponent'))

export default function Home() {
  const [isVisible, setIsVisible] = useState(false)
  return (
    <main>
      <button onClick={() => {setIsVisible(true)}}>Show</button>
      {isVisible && <HeavyComponent />} 
    </main>
  );
}
```

When loading components dynamically, as a second argument to the dynamic function we can pass an options object. Here we can pass a loading function for showing a loading indicator when the component is being downloaded as show:

```TSX
'use client';

import { useState } from "react";
import dynamic from "next/dynamic";
const HeavyComponent = dynamic(() => import('./components/HeavyComponent/HeavyComponent'), {loading: () => <p>Loading...</p>})

export default function Home() {
  const [isVisible, setIsVisible] = useState(false)
  return (
    <main>
      <button onClick={() => {setIsVisible(true)}}>Show</button>
      {isVisible && <HeavyComponent />} 
    </main>
  );
}
```
The other property that we have in this options object is ssr. When importing client components, by default they are pre-rendered on the server. Sometimes this can cause issues because when trying to access certain apis from the server, and they're not available you might end up getting errors. In such situations, you can disable pre-rendering on the server by setting ssr to false as shown:

```TSX
"use client";

import { useState } from "react";
import dynamic from "next/dynamic";
const HeavyComponent = dynamic(
  () => import("./components/HeavyComponent/HeavyComponent"),
  { loading: () => <p>Loading...</p>, ssr: false }
);

export default function Home() {
  const [isVisible, setIsVisible] = useState(false);
  return (
    <main>
      <button
        onClick={() => {
          setIsVisible(true);
        }}
      >
        Show
      </button>
      {isVisible && <HeavyComponent />}
    </main>
  );
}

```

## Lazy Loading third-party Libraries

We can use the lodash library which is a popular utility library for JavaScript to demonstrate lazy loading third-party libraries. This library is used to manipulate objects and arrays.

Say we wanted to sort an array of users on the click of a button using this library, lazy loading it becomes a necessity if we want to factor optimization.

To lazy load this library we should call the import function inside the click handler as shown below:

```TSX
"use client";


export default function Home() {
  return (
    <main>
      <button
        onClick={async () => {
          const _ = (await import('lodash')).default;
          
          const users = [
            {name: 'c'},
            {name: 'b'},
            {name: 'a'},
          ]

          const sorted = _.orderBy(users, ['name']);
          console.log(sorted);
        }}
      >
        Show
      </button>
    </main>
  );
}
```