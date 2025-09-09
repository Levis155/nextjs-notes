# Creating Migrations

As we define or change our models we have to create migrations. These keep our database schema in sync with our prisma schema.

To create a migration run the following command in the terminal:

```bash
npx prisma migrate dev
```

Upon running this command, we're prompted to give a name to the migration. This name should describe the changes to the schema that the new migration brings.