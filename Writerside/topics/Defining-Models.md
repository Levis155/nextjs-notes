# Defining Models

Models are entities of our application domain e.g. product, customer, cart e.t.c.

These models are defined in the **schema.prisma** file and use the PascalCase naming convention.

Models typically have properties or fields with their types defined and attributes assigned.

**Example:**

```tsx
generator client {
  provider = "prisma-client-js"
  output   = "../app/generated/prisma"
}

datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int     @id @default(autoincrement())
  email     String  @unique
  name      String
  followers Int     @default(0)
  isActive  Boolean @default(true)
}

```