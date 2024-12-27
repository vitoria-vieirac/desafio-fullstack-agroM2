# desafio-fullstack-agroM2

Projeto desenvolvido com TypeScript, utilizando Nextjs no frontend e Nestjs no backend, PrismaORM e banco de dados PostgreSQL.

Desenvolvimento de uma aplicação voltada para o gerenciamento de colheitas de soja.

Para baixar as dependências necessárias:
npm install

Para gerar o banco de dados com prisma:
#npm install prisma @prisma/client
#npx prisma init

1. Configurar banco de dados no .env:
DATABASE_URL="postgresql://usuario:senha@localhost:5432/meu_banco?schema=public"

2. schema.prisma:

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int       @id @default(autoincrement())
  name      String
  email     String    @unique
  password  String
  harvests  Harvest[]
}

model Harvest {
  id             Int      @id @default(autoincrement())
  date           DateTime @default(now())
  location       String
  quantityInTons Float
  seed           String
  fertilizer     String
  userId         Int?
  user           User?    @relation(fields: [userId], references: [id])
}

3. npx prisma migrate dev --name init
4. npx prisma migrate
5. Rodar o projeto backend : npm run dev (estar dentro da pasta backend-nest)
6. Rodar o projeto frontend: npm run dev (estar dentro da pasta frontend-next)

