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