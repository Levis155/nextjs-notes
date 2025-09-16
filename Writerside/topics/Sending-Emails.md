# Sending Emails With React Email

## Setting Up React Email

React Email is a very powerful library for sending emails with React and TypeScript. It gives us a bunch of components for creating html emails, an email preview tool, and a function for sending emails.

Follow the following steps to set up React Email:

- Install React Email alongside its components by running the following command:

```bash
npm i react-email @react-email/components
```

- Add a custom command for previewing your emails in the `package.json` file: 

```JSON
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "preview-email": "email dev -p 3030"
  },
```

- For the final setup step, create an emails folder in the root of your project where you'll add react components that represent your email templates.

## Creating an Email Template

In the emails folder create a file e.g. `WelcomeTemplate.tsx` that returns a React component representing a template of the email.

**./emails/WelcomeTemplate.tsx:**

```TSX
import React from 'react'
import { Html, Body, Container, Text, Link, Preview} from "@react-email/components"

const WelcomeTemplate = ({name}: {name: string}) => {
  return (
    <Html>
        <Preview>Welcome Aboard!</Preview>
        <Body>
            <Container>
                <Text>Hello World!</Text>
                <Link href='https://www.random-site.com'>Random Site</Link>
            </Container>
        </Body>
    </Html>
  )
}

export default WelcomeTemplate
```

## Previewing Emails

React-Email gives us a tool for previewing emails. To use this tool we have to run `npm run preview-email`. Before running this command however add `react-email` folder to your .gitignore file to prevent it from being tracked by git. This is because the above command creates an application for viewing emails with thousands of files which we don't want to track as they're not part of our source code.

## Styling Emails

There are two ways to style email templates:

- Using CSS properties

```TSX
import React, { CSSProperties } from 'react'
import { Html, Body, Container, Text, Link, Preview} from "@react-email/components"

const WelcomeTemplate = ({name}: {name: string}) => {
  return (
    <Html>
        <Preview>Welcome Aboard!</Preview>
        <Body style={body}>
            <Container>
                <Text style={heading}>Hello World!</Text>
                <Link href='https://www.random-site.com'>Random Site</Link>
            </Container>
        </Body>
    </Html>
  )
}

const body: CSSProperties = {
    background: "#fff"
}

const heading: CSSProperties = {
    fontSize: '32px'
}

export default WelcomeTemplate

```

- Using Tailwind

```TSX
import {
  Html,
  Body,
  Container,
  Text,
  Link,
  Preview,
  Tailwind,
} from "@react-email/components";

const WelcomeTemplate = ({name}: {name: string}) => {
  return (
    <Html>
      <Preview>Welcome Aboard!</Preview>
      <Tailwind>
        <Body className="bg-white">
          <Container>
            <Text className="font-bold text-3xl">Hello World!</Text>
            <Link href="https://www.random-site.com">Random Site</Link>
          </Container>
        </Body>
      </Tailwind>
    </Html>
  );
};

export default WelcomeTemplate;

```

## Sending Emails

For sending emails you can choose from a variety of services. One particular service that facilitates sending of emails is **Resend.**

To get started with using Resend, follow the following steps:

- Head over to [resend.com](https://resend.com/) and create an account.

- Once logged in you can generate an API key in the homepage and save this key in your .env file 
`RESEND_API_KEY='YOUR RESEND API KEY'`

- Install Resend by running the following command:

```Bash
npm i resend@1.0.0
```

- Create an api endpoint for sending emails. 
**app/api/send-email/route.tsx:**

```TSX
import WelcomeTemplate from "@/emails/WelcomeTemplate";
import { NextResponse } from "next/server";
import { Resend } from "resend";

const resend = new Resend(process.env.RESEND_API_KEY);

export async function POST() {
    resend.emails.send({
        from: 'example@your-domain.com',
        to: "random-email@gmail.com",
        subject: "RANDOM SUBJECT",
        react: <WelcomeTemplate name="John" />
    })

    return NextResponse.json({});
}
```

> Note that this is just for demonstration as in a real-world application you wouldn't have an endpoint for sending emails, but instead sending emails should be part of your business operations. e.g. when a customer places an order they would typically receive a confirmation email.

> Another thing to note is that the 'from' email should be from a domain that you own (You cannot use free services such as gmail, yahoo e.t.c). After obtaining your domain you should log in to Resend and configure it in the Domains page.
