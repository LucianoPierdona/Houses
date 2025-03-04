# Migration `20210201014510-added-houses-table`

This migration has been generated at 1/31/2021, 10:45:10 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE "houses" (
"id" SERIAL,
    "user_id" TEXT NOT NULL,
    "image" TEXT NOT NULL,
    "latitude" DECIMAL(65,30) NOT NULL,
    "longitude" DECIMAL(65,30) NOT NULL,
    "address" TEXT NOT NULL,
    "bedrooms" INTEGER NOT NULL,
    "created_at" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
    "updated_at" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,

    PRIMARY KEY ("id")
)

CREATE INDEX "houses.userId" ON "houses"("user_id")
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration ..20210201014510-added-houses-table
--- datamodel.dml
+++ datamodel.dml
@@ -1,0 +1,26 @@
+// This is your Prisma schema file,
+// learn more about it in the docs: https://pris.ly/d/prisma-schema
+
+datasource db {
+  provider = "postgresql"
+  url = "***"
+}
+
+generator client {
+  provider = "prisma-client-js"
+}
+
+model House {
+  id        Int      @id @default(autoincrement())
+  userId    String   @map(name: "user_id")
+  image     String
+  latitude  Float
+  longitude Float
+  address   String
+  bedrooms  Int
+  createdAt DateTime @default(now()) @map(name: "created_at")
+  updatedAt DateTime @default(now()) @map(name: "updated_at")
+
+  @@index([userId], name: "houses.userId")
+  @@map(name: "houses")
+}
```


