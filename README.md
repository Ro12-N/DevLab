# 🤖 AI Project Builder - DevLab

![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?logo=typescript)
![Prisma](https://img.shields.io/badge/Prisma-5.0-2D3748?logo=prisma)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT4-412991?logo=openai)
![Stripe](https://img.shields.io/badge/Stripe-Payments-008CDD?logo=stripe)

> An AI-powered platform that generates complete Next.js projects from natural language descriptions. Uses OpenAI for code generation and E2B sandboxes for live preview.

## ✨ Features

- 🤖 **AI Code Generation** - Describe your app, AI builds it
- 📦 **E2B Sandbox** - Live preview in isolated environment
- 🔄 **Background Jobs** - Inngest for async processing
- 💳 **Subscription Plans** - Free (5 projects) / Pro (unlimited)
- 🔐 **Authentication** - Clerk with Google/GitHub OAuth
- 📁 **File Explorer** - Browse generated project files
- 🖥️ **Terminal** - Run commands in sandbox
- 🎨 **Responsive UI** - Tailwind CSS + Shadcn

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| Frontend | Next.js 15, React 19, Tailwind CSS |
| Database | PostgreSQL, Prisma ORM |
| Auth | Clerk |
| AI | OpenAI API / Gemini API |
| Background Jobs | Inngest |
| Sandbox | E2B |
| Payments | Stripe |
| Deployment | Vercel |

## 📊 Database Schema

```prisma
model User {
  id          String    @id @default(cuid())
  email       String    @unique
  name        String
  role        Role      @default(FREE)
  projects    Project[]
  stripeCustomerId String?
  createdAt   DateTime  @default(now())
}

model Project {
  id          String    @id @default(cuid())
  name        String
  description String
  status      Status    @default(GENERATING)
  files       Json
  userId      String
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt
}

enum Role {
  FREE
  PRO
}

enum Status {
  GENERATING
  READY
  FAILED
}
