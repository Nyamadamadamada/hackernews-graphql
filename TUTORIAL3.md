# Adding a Database

PrismaとSQLiteを使用してプロジェクトを設定する
```
npm install prisma --save-dev
npm install @prisma/client
```

次に、Prisma CLIを使用して、プロジェクトのPrismaを初期化します。
```
npx prisma init
```

Next steps:
1. Set the DATABASE_URL in the .env file to point to your existing database. If your database has no tables yet, read https://pris.ly/d/getting-started
2. Set the provider of the datasource block in schema.prisma to match your database: postgresql, mysql, sqlite, sqlserver or mongodb (Preview).
3. Run prisma db pull to turn your database schema into a Prisma schema.
4. Run prisma generate to generate the Prisma Client. You can then start querying your database.


```.../hackernews-node/prisma/schema.prisma
// 1
datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}

// 2
generator client {
  provider = "prisma-client-js"
}

// 3
model Link {
  id          Int      @id @default(autoincrement())
  createdAt   DateTime @default(now())
  description String
  url         String
}
```

```
npx prisma migrate dev
```