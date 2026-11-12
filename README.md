# Mazzers

*Mazzers* is a goal and daily-task tracker built with *Next.js 16 (App Router), **React 19* and *TypeScript*. Users create an account, sign in and manage their tasks in a dashboard with tags, search, filters and progress stats.

> Learning project, still in development. Authentication is a prototype (see [Current limitations](#current-limitations)).

## Features

- *Landing page* with animated illustrations (Lottie) and a call to action
- *Sign up and sign in* forms validated with Zod and React Hook Form
- *JWT sessions*: tokens are signed with jose (HS256, 7-day expiry) and stored in an httpOnly cookie through a Server Action
- *Protected routes*: middleware redirects guests away from /your-goals and signed-in users away from the login page
- *Password hashing* with bcryptjs in the register API route
- *Task dashboard*
  - Add tasks, mark them completed and delete them
  - Tag tasks as Work, Home or Health (shadcn/ui dropdown)
  - Live search and All / Active / Completed filters
  - Stats for total, pending and completed tasks, plus a daily completion progress bar

## Tech stack

| Area | Tools |
| --- | --- |
| Framework | Next.js 16 (App Router), React 19 |
| Language | TypeScript |
| Forms and validation | React Hook Form, Zod |
| Auth | jose (JWT), bcryptjs, httpOnly cookies, Next.js middleware, Server Actions |
| Styling | Tailwind CSS v4, CSS Modules |
| UI | shadcn/ui, Base UI, lucide-react, lottie-react |

## Getting started

Requirements: Node.js 20+ and npm.

bash
git clone <repo-url>
cd mazzers
npm install


Create a .env.local file in the project root:

bash
JWT_SECRET=replace-with-a-random-string-of-at-least-32-characters


Then start the dev server:

bash
npm run dev


Open [http://localhost:3000](http://localhost:3000).

## Scripts

| Command | What it does |
| --- | --- |
| npm run dev | Start the development server |
| npm run build | Production build |
| npm start | Serve the production build |
| npm run lint | Run ESLint |

## Project structure


app/
  page.tsx                  Landing page
  register-page/            Sign-up form
  login-page/               Sign-in form
  your-goals/               Task dashboard (protected)
  actions/auth.ts           Server Actions: create session, log out
  api/auth/register/        POST: validate input, hash password, issue token
  api/auth/logout/          Logout route (in progress)
  Animations/               Lottie JSON animations, logo and icons
components/ui/              shadcn/ui components (button, dropdown-menu, progress)
lib/auth.ts                 JWT helpers: createToken, verifyToken, getSession
middleware.ts               Route protection


## Current limitations

- There is no database yet. Accounts are kept in the browser's localStorage and tasks only live in memory, so they reset on refresh.
- The register API route hashes the password but does not save the user yet.
