# Configuring Google Provider

Configuring Google Provider involves a number of steps:

## Creating an Account on Google Cloud Platform

To get started with configuring Google provider head over to [Google Cloud Platform](https://console.cloud.google.com/) and create an account. 

After creating an account navigate to the [credentials page](https://console.cloud.google.com/apis/credentials) to start configuration. 

## Creating a Project and Configuring the Consent Screen

Locate and click on the New Project button and create a new project. 

Next you need to configure the consent screen. Click on the configure consent screen button and follow the steps. Here you get to configure the user type, the consent screen preview, authorized domains, the developer's contact info, scopes, and test users. 

## Creating an OAuth Client

Navigate to the overview page and click on create OAuth client button. OAuth is short for Open Authentication, and it's a standard authentication protocol that a lot of websites like Google, Facebook, Twitter e.t.c implement.

Here you configure the following:

- Application type (typically Web Application)
- Application Name
- Authorized JavaScript Origins - Typically the root of your website.
- Authorized redirect URIs. This is the URL that Google will use to send the user back to your application. You can get this URL for the [providers page](https://authjs.dev/getting-started/providers/google) in Auth.js official documentation website.

After creating the OAuth client you're issued with the client ID along with the client secret. These values should be copied and stored in a .env file.

## Creating a Google Provider

Next you need to create a Google Provider. In the route file import Google provider from the next-auth package and set it as one of the providers as shown below:

**/api/auth/[...nextauth]/route.ts:**

```TS
import NextAuth from "next-auth";
import GoogleProvider from "next-auth/providers/google"

const handler = NextAuth({
    providers: [
        GoogleProvider({
            clientId: process.env.GOOGLE_CLIENT_ID,
            clientSecret: process.env.GOOGLE_CLIENT_SECRET,
        })
    ]
})

export { handler as GET, handler as POST}
```

## Adding a Sign-in Link

For the final step add the sign-in link to the navbar as follows:

**app/Navbar.tsx:**

```TSX
import Link from 'next/link'
import React from 'react'

const Navbar = () => {
  return (
    <div className='flex bg-slate-200 p-5 space-x-3'>
      <Link href="/" className='mr-5'>Next.js</Link>
      <Link href="/users">Users</Link>
      <Link href="/api/auth/signin">Login</Link>
    </div>
  )
}

export default Navbar

```