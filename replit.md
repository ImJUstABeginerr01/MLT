# UKOM Exam Preparation Platform

## Overview

This is a professional exam preparation platform for UKOM (Uji Kompetensi) certification. The application provides two study modes:

1. **Tryout Mode**: Practice exams organized by subject with 100 questions per section
2. **Simulasi Mode**: Full simulation of the actual UKOM exam with 180 questions and 180-minute timer

The platform includes features such as timed exams, question bookmarking, progress tracking, answer submission, detailed result analysis, and an admin panel for question management.

## User Preferences

Preferred communication style: Simple, everyday language.

## Local Development Setup

The user prefers to run this application on their local computer. See `SETUP_LOCAL.md` for complete instructions including:
- System requirements (Node.js, PostgreSQL)
- Database setup
- Environment variable configuration
- Running development server locally

Quick commands:
```bash
npm install              # Install dependencies
npm run db:push         # Setup database schema
npm run dev             # Start development server (http://localhost:5000)
```

## System Architecture

### Frontend Architecture

**Framework**: React 18+ with TypeScript using Vite as the build tool

**Routing**: Client-side routing with Wouter (lightweight alternative to React Router)

**State Management**:
- TanStack Query (React Query) for server state management and caching
- React Hook Form with Zod validation for form state
- Local component state with React hooks for UI interactions

**UI Component Library**: Shadcn/ui with Radix UI primitives
- Design system follows Material Design principles with productivity-focused adaptations
- Uses Tailwind CSS for styling with custom theme configuration
- Typography uses Inter font from Google Fonts
- Consistent spacing system using Tailwind units (2, 4, 6, 8, 12)

**Key Design Decisions**:
- Component-based architecture with reusable UI primitives
- Type-safe API communication through shared schema definitions
- Responsive design with mobile-first approach
- Accessibility built-in through Radix UI primitives

### Backend Architecture

**Framework**: Express.js (Node.js) with TypeScript

**API Design**: RESTful API endpoints organized by resource type:
- `/api/auth/*` - Authentication endpoints
- `/api/questions/*` - Question CRUD operations
- `/api/exam-sessions/*` - Exam session management
- `/api/exam-answers/*` - Answer tracking

**Authentication**: Replit Auth integration using OpenID Connect (OIDC)
- Passport.js strategy for authentication flow
- Session-based authentication with PostgreSQL session store
- Automatic user profile creation/update from OIDC claims
- Admin role management through user database

**Data Access Layer**: Repository pattern implementation through `IStorage` interface
- Abstraction layer between business logic and database
- Enables testing and potential database switching
- Type-safe operations using Drizzle ORM types

### Database Architecture

**ORM**: Drizzle ORM with PostgreSQL dialect

**Database Provider**: Neon Serverless PostgreSQL with WebSocket support

**Schema Design**:

1. **Users Table**: Stores user profiles from Replit Auth
   - Auto-generated UUID primary keys
   - Email uniqueness constraint
   - Admin flag for access control
   - Timestamps for audit trail

2. **Questions Table**: Question bank organization
   - Subject categorization (Hematologi, Kimia Klinik, etc.)
   - Section numbering within subjects
   - Multiple choice format (4 options: A, B, C, D)
   - Correct answer storage
   - Optional explanation field

3. **Exam Sessions Table**: Tracks exam attempts
   - User association via foreign key
   - Mode differentiation (tryout vs simulasi)
   - Subject and section tracking
   - Start/end timestamps
   - Completion status

4. **Exam Answers Table**: Individual answer tracking
   - Session association
   - Question association
   - Selected answer storage
   - Bookmark functionality
   - Answer correctness flag

5. **Sessions Table**: Authentication session storage
   - Used by connect-pg-simple for Express sessions
   - Automatic expiration handling

**Migration Strategy**: Drizzle Kit for schema migrations
- Schema definitions in TypeScript
- Type-safe migrations
- Version controlled schema changes

### Development & Production Setup

**Development**:
- Vite dev server with HMR (Hot Module Replacement)
- Server-side rendering for HTML template
- Development-specific Replit plugins (Cartographer, Dev Banner)
- Runtime error overlay for debugging

**Production**:
- Vite builds optimized client bundle
- esbuild bundles server code for Node.js
- Static file serving from dist/public
- SPA fallback to index.html

**Build Process**:
- Client: Vite build with React plugin
- Server: esbuild bundle with ESM output
- Shared types between client and server

## External Dependencies

### Core Infrastructure

**Neon Database**: Serverless PostgreSQL database
- WebSocket connection support for serverless environments
- Automatic scaling and connection pooling
- DATABASE_URL environment variable for connection string

**Replit Authentication**: OAuth 2.0 / OpenID Connect provider
- ISSUER_URL environment variable (defaults to https://replit.com/oidc)
- REPL_ID for client identification
- SESSION_SECRET for session encryption
- Automatic user profile synchronization

### Third-Party Libraries

**UI & Styling**:
- Radix UI: Accessible component primitives
- Tailwind CSS: Utility-first CSS framework
- class-variance-authority: Type-safe variant styling
- Lucide React: Icon library

**Forms & Validation**:
- React Hook Form: Performant form state management
- Zod: Schema validation library
- @hookform/resolvers: Integration between React Hook Form and Zod

**Data Management**:
- TanStack Query: Server state management
- Drizzle ORM: Type-safe database ORM
- drizzle-zod: Schema validation integration

**Authentication**:
- Passport.js: Authentication middleware
- openid-client: OpenID Connect client
- express-session: Session management
- connect-pg-simple: PostgreSQL session store

**Development Tools**:
- Vite: Build tool and dev server
- TypeScript: Type safety
- ESBuild: Fast JavaScript bundler
- tsx: TypeScript execution for development