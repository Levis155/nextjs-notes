# Protecting Routes

To protect our routes we usually use middleware. With middleware, we can run code before a request is completed. We can therefore create a middleware function that gets executed on every request that checks the user session and redirects unauthenticated users to the login page.

To do this, create a `middleware.ts` file in the root of your project. This is where you will import the `auth()` function from your `auth.ts` configuration file and configure logic for your protected routes. 

**/middleware.ts:**

```TS
import { auth } from "@/auth"

export default auth((req) => {
  // If the user is not authenticated, redirect them to the login page.
  if (!req.auth && req.nextUrl.pathname !== "/login") {
    const newUrl = new URL("/login", req.nextUrl.origin);
    return Response.redirect(newUrl);
  }

  // If authenticated, the request proceeds.
});

// Configure which paths to protect.
export const config = {
  matcher: ["/users/:id*"], // Protect all routes under `/users`.
};

```