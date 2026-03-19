# ClassConnect Pro

ClassConnect Pro is a production-style starter for a school or college attendance SaaS platform built with Next.js 14 App Router, TypeScript, Tailwind CSS, Prisma, PostgreSQL, and Auth.js.

This repository gives you:

- modern responsive dashboard UI
- Prisma schema for multi-school attendance SaaS
- demo auth setup with seeded users
- routes for dashboard, attendance, reports, chat, admin, premium, schedule, insights, and leaderboard
- `.env.example`, Docker Compose, and seed data

## 1. What you need before starting

Install these on your computer:

1. Node.js 20 or later
2. npm
3. Docker Desktop
4. Git
5. VS Code

Check versions:

```powershell
node -v
npm -v
docker -v
git --version
```

## 2. Open the project

If the project is already in this folder:

```powershell
cd "C:\Users\dnyan\OneDrive\Documents\New project"
```

## 3. Install dependencies

```powershell
npm install
```

## 4. Start PostgreSQL with Docker

```powershell
docker compose up -d
```

This starts PostgreSQL on:

- host: `localhost`
- port: `5432`
- database: `classconnect`
- user: `postgres`
- password: `postgres`

## 5. Create environment variables

Copy `.env.example` to `.env`.

On PowerShell:

```powershell
Copy-Item .env.example .env
```

For local development, the default database URL already points to Docker PostgreSQL.

## 6. Push the Prisma schema

```powershell
npm run db:push
```

If you want migrations instead:

```powershell
npm run db:migrate
```

## 7. Seed demo data

```powershell
npm run db:seed
```

Demo login accounts:

- `admin@classconnect.dev` / `password123`
- `teacher@classconnect.dev` / `password123`
- `parent@classconnect.dev` / `password123`
- `student@classconnect.dev` / `password123`

## 8. Run the app

```powershell
npm run dev
```

Open:

- [http://localhost:3000](http://localhost:3000)

## 9. Project structure

```text
prisma/
  schema.prisma
  seed.ts
src/
  app/
    admin/
    api/auth/[...nextauth]/
    attendance/[batch]/[class]/
    batches/
    chat/[roomId]/
    dashboard/
    insights/
    leaderboard/
    login/
    premium/
    reports/
    schedule/
    globals.css
    layout.tsx
    manifest.ts
    page.tsx
  components/
    charts/
    dashboard/
    forms/
    layout/
    providers/
    ui/
  i18n/
    request.ts
  lib/
    constants.ts
    demo-data.ts
    prisma.ts
    utils.ts
  messages/
    en.json
    hi.json
  types/
    next-auth.d.ts
src/auth.ts
```

## 10. How to build this project from basic

Follow this order. Do not jump randomly between features.

### Step A: Build the base app

1. Create the Next.js app with TypeScript.
2. Install Tailwind CSS.
3. Create the global layout and navigation.
4. Build the landing page.
5. Build shared UI components like `Button`, `Card`, and `Input`.

You already have that foundation in this repo.

### Step B: Build the database

1. Open [prisma/schema.prisma](/C:/Users/dnyan/OneDrive/Documents/New%20project/prisma/schema.prisma)
2. Understand the main models:
   `School`, `User`, `Batch`, `AttendanceSession`, `Attendance`, `Subscription`, `AuditLog`
3. Run `npm run db:push`
4. Run `npm run db:seed`

Start simple:

- one school
- one admin
- one teacher
- one parent
- one student
- one batch
- one attendance session

### Step C: Build authentication

1. Open [src/auth.ts](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/auth.ts)
2. This file uses Auth.js credentials login.
3. Passwords are stored as hashes in Prisma.
4. Login form is in [src/components/forms/login-form.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/components/forms/login-form.tsx)
5. Login page is in [src/app/login/page.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/app/login/page.tsx)

If you want Google login later, add another Auth.js provider after credentials login works.

### Step D: Build the dashboard

1. Open [src/app/dashboard/page.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/app/dashboard/page.tsx)
2. Replace demo data from [src/lib/demo-data.ts](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/lib/demo-data.ts) with Prisma queries.
3. Show:
   overall attendance,
   active batches,
   risk students,
   parent engagement.

### Step E: Build attendance flow

1. Open [src/app/attendance/[batch]/[class]/page.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/app/attendance/[batch]/[class]/page.tsx)
2. Replace static student list with Prisma data.
3. Add a form or server action to save attendance.
4. Create one `AttendanceSession` per class/date.
5. Create one `Attendance` row per student.

Build features in this order:

1. manual attendance
2. photo capture
3. GPS validation
4. offline queue
5. WebAuthn
6. hardware integrations

### Step F: Build reports

1. Open [src/app/reports/page.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/app/reports/page.tsx)
2. Connect it to Prisma attendance data.
3. Add export actions for PDF and Excel.
4. Add Google Sheets sync after local export works.

### Step G: Build admin tools

1. Open [src/app/admin/page.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/app/admin/page.tsx)
2. Add:
   school branding,
   role management,
   audit logs,
   2FA settings,
   plan limits.

### Step H: Build premium billing

1. Open [src/app/premium/page.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/app/premium/page.tsx)
2. Add Stripe checkout session API route.
3. Add webhook route.
4. Save subscription data in `Subscription`.
5. Restrict premium features based on school plan.

### Step I: Build communication

1. Open [src/app/chat/[roomId]/page.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/app/chat/[roomId]/page.tsx)
2. Connect Socket.io server and client.
3. Save messages to `ChatMessage`.
4. Add in-app notifications first.
5. Add email, SMS, push, WhatsApp later.

### Step J: Build AI

1. Open [src/app/insights/page.tsx](/C:/Users/dnyan/OneDrive/Documents/New%20project/src/app/insights/page.tsx)
2. Start with rule-based alerts:
   below 75% attendance,
   repeated absences,
   Friday pattern drops.
3. After that, call OpenAI to generate summaries or improvement tips.

Do not start with AI prediction before attendance data is reliable.

## 11. What is real now vs placeholder

### Already implemented in this starter

- app structure
- responsive UI
- route structure
- Prisma schema
- demo seed data
- Auth.js credentials flow
- bilingual message files
- plan page shell
- attendance page shell
- reports page shell

### Placeholder integrations you still need to connect

- Stripe
- Twilio
- Resend
- OpenAI
- Google Calendar
- Zoom
- WhatsApp Business API
- Firebase Cloud Messaging
- WebAuthn device registration
- WebUSB hardware communication
- IndexedDB offline sync

## 12. Best next coding task

If you want to continue building properly, do this next:

1. replace demo dashboard data with Prisma queries
2. save attendance records to the database
3. protect routes based on session and role
4. add admin school settings
5. add Stripe billing

## 13. Deployment

For Vercel deployment later:

1. push code to GitHub
2. create a hosted PostgreSQL database
3. copy production environment variables
4. run Prisma migrations
5. deploy on Vercel

## 14. Important note

This repo is a strong starter, not the fully finished enterprise product from the original giant specification. Features like WhatsApp, Zoom, Stripe webhooks, 2FA enforcement, passkeys, WebUSB devices, FCM, and AI workflows are complex integrations that should be added on top of this foundation one by one.
