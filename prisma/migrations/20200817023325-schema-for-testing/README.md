# Migration `20200817023325-schema-for-testing`

This migration has been generated by jeongsd at 8/17/2020, 11:33:25 AM. You can check out the
[state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;

CREATE TABLE "Todo" (
"id" TEXT NOT NULL,
"text" TEXT NOT NULL,
"isCompleted" BOOLEAN NOT NULL DEFAULT false,
PRIMARY KEY ("id"))

CREATE TABLE "User" (
"id" INTEGER NOT NULL,
"email" TEXT NOT NULL,
PRIMARY KEY ("id"))

CREATE TABLE "Profile" (
"firstname" TEXT NOT NULL,
"lastname" TEXT NOT NULL)

CREATE UNIQUE INDEX "User.email_unique" ON "User"("email")

CREATE UNIQUE INDEX "Profile.firstname_lastname_unique" ON "Profile"("firstname","lastname")

PRAGMA foreign_key_check;

PRAGMA foreign_keys=ON;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration ..20200817023325-schema-for-testing
--- datamodel.dml
+++ datamodel.dml
@@ -1,0 +1,27 @@
+datasource sqlite {
+  provider = "sqlite"
+  url = "***"
+}
+
+generator client {
+  provider = "prisma-client-js"
+}
+
+model Todo {
+  id          String  @id
+  text        String
+  isCompleted Boolean @default(false)
+}
+
+model User {
+  id    Int    @id
+  email String @unique
+}
+
+
+model Profile {
+  firstname String
+  lastname String
+
+  @@unique([firstname, lastname])
+}
```