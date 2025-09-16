# Sending Emails

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

const WelcomeTemplate = () => {
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

const WelcomeTemplate = () => {
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

const WelcomeTemplate = () => {
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
