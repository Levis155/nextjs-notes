# Handling Unexpected Errors

By default, whenever an unexpected error occurs a generic error page is shown. We can customize this by adding a special file in the app folder called `error.tsx`. In this file we should create and export a component that should be rendered whenever any of our pages experiences an unexpected error. This component has to be a client component.

**app/error.tsx:**

```TSX
'use client';
import React from 'react'

const ErrorPage = () => {
  return (
    <div>
      An unexpected error has occurred.
    </div>
  )
}

export default ErrorPage

```

There are a couple of things to note about this error file:

- We can have error files at different levels of our application's routes. For instance, we can have an error file in the users folder and this file catches any errors that happen in any or the routes under users folder.
- In this file we cannot capture any errors that occur within the root layout `layout.tsx`. A separate error file `global-error.tsx` is employed to achieve this.
- We can access the error that has occurred by passing the error props in the component being returned as shown below:
```TSX
'use client';
import React from 'react'

interface Props {
    error: Error;
}

const ErrorPage = ({error}: Props) => {
    console.log(error);
  return (
    <div>
      An unexpected error has occurred.
    </div>
  )
}

export default ErrorPage
```

- In instances where the error is temporary, we can give the user a retry option by passing the reset property.

```TSX
"use client";
import React from "react";

interface Props {
  error: Error;
  reset: () => void;
}

const ErrorPage = ({ error, reset }: Props) => {
  console.log(error);
  return (
    <>
      <div>An unexpected error has occurred.</div>
      <button className="btn" onClick={() => reset()}>Retry</button>
    </>
  );
};

export default ErrorPage;

```
Since we're handling a click event it is now clear why this component has to be a client-side component.