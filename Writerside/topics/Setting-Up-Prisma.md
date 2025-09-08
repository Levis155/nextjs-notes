# Setting Up Prisma

Prisma is an Object Relational Mapping (ORM) tool. ORMs sit between our applications and a database. We use them to send queries to the database.

Start by installing Prisma into your project using the following command:

```bash
npm i prisma
```

Then run the following command to set up Prisma:

```Bash
npx prisma init
```

The above command does a couple of things:
- Creates a Prisma folder with a schema file in the root directory of your project
- Creates a `.env` file where the database URL is stored.

By default, Prisma uses Postgres hence we need to modify the connection string in the .env file to something compatible with MYSQL. e.g:

`mysql://root:MyP@ssw0rd@localhost:3306/nextapp`

The default provider in the prisma file is Postgres  but this can be modified to the database you're working with i.e. `mysql` in our scenario.