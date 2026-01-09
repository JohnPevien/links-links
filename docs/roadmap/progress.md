# Links Links - Progress Tracker

## Project Overview
A dynamic links website where users can add collections of links, stored in a database.

## Current Milestone: Dynamic Links with SQLite

### Completed Tasks
- [x] Research and recommend cloud database options (Turso, Supabase, Neon)

### In Progress
- [x] Initialize Prisma with SQLite
- [x] Define Database Schema (Category and Link models)
- [ ] Create a migration and seed script to import data from jmdy.html
- [ ] Implement the main page in Next.js (src/app/page.tsx) to fetch data from the DB
- [ ] Add a simple UI for adding/editing links and categories
- [ ] (Optional) Setup Turso for cloud deployment

### Database Schema Design

#### Models
```prisma
model Category {
  id        String   @id @default(cuid())
  name      String   @unique
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  links     Link[]
}

model Link {
  id         String   @id @default(cuid())
  title      String
  url        String
  categoryId String
  category   Category @relation(fields: [categoryId], references: [id])
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt
}
```

#### Future: User Model (Next Milestone)
```prisma
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  password  String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  categories Category[]
}

// Update Category model to include user ownership
model Category {
  id        String   @id @default(cuid())
  name      String
  userId    String
  user      User     @relation(fields: [userId], references: [id])
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  links     Link[]
}
```

## Next Milestone: User Authentication

### Planned Features
- [ ] User registration and login
- [ ] User-specific link collections
- [ ] Session management
- [ ] Protected routes for admin actions

### Authentication Options to Consider
1. **NextAuth.js (Auth.js)** - Recommended for Next.js
   - Easy integration with Next.js
   - Supports multiple providers (email/password, OAuth)
   - Built-in session management
   - TypeScript support

2. **Clerk** - Complete authentication solution
   - Drop-in authentication
   - User management UI
   - Free tier available

3. **Supabase Auth** - If using Supabase as database
   - Built-in authentication
   - Row-level security
   - Free tier available

### Recommended Approach
**NextAuth.js with Credentials Provider** - Simplest for email/password auth without external dependencies.

## Cloud Database Options

### Turso (Recommended)
- **Type**: SQLite-compatible (LibSQL)
- **Free Tier**: 500 rows, 9 GiB storage, 3 databases
- **Pros**: Fast edge deployment, SQLite compatible, generous free tier
- **Cons**: Newer platform, smaller community

### Supabase
- **Type**: PostgreSQL
- **Free Tier**: 500 MB database, 1 GB bandwidth, 2 concurrent connections
- **Pros**: Mature platform, built-in auth, real-time features
- **Cons**: PostgreSQL (not SQLite), connection limits on free tier

### Neon
- **Type**: PostgreSQL
- **Free Tier**: 3 projects, 0.5 GB storage, 300 hours compute
- **Pros**: Serverless, fast, auto-scaling
- **Cons**: PostgreSQL (not SQLite), compute hours limit

## Technology Stack
- **Framework**: Next.js 16 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **Database**: SQLite (local) / Turso (cloud)
- **ORM**: Prisma
- **Authentication (Future)**: NextAuth.js

## File Structure
```
links-links/
├── docs/
│   └── roadmap/
│       └── progress.md
├── prisma/
│   ├── schema.prisma
│   ├── seed.ts
│   └── dev.db
├── src/
│   ├── app/
│   │   ├── page.tsx
│   │   ├── layout.tsx
│   │   └── globals.css
│   ├── components/
│   │   ├── LinkCard.tsx
│   │   ├── CategoryCard.tsx
│   │   └── AdminPanel.tsx
│   └── lib/
│       └── prisma.ts
├── jmdy.html
├── package.json
└── PROGRESS.md
```

## Notes
- Keep the existing jmdy.html as reference for the seed data
- Use the existing Tailwind CSS configuration from jmdy.html
- Maintain the dark theme styling
- Ensure responsive design for mobile devices
