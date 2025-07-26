# replit.md

## Overview

This is a comprehensive OSINT (Open Source Intelligence) investigation platform built with a full-stack TypeScript architecture. The application allows users to conduct automated digital forensics investigations on usernames, emails, phone numbers, and domains using multiple OSINT tools. It features a modern React frontend with Tailwind CSS and shadcn/ui components, an Express.js backend, and PostgreSQL database with Drizzle ORM.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

The application follows a monorepo structure with clear separation between client, server, and shared code:

- **Frontend**: React SPA with TypeScript, served from `/client` directory
- **Backend**: Express.js REST API server in `/server` directory  
- **Shared**: Common schemas and types in `/shared` directory
- **Database**: PostgreSQL with Drizzle ORM for type-safe database operations
- **Authentication**: Replit-based OIDC authentication with session management
- **Build System**: Vite for frontend bundling, esbuild for backend compilation

## Key Components

### Frontend Architecture
- **React Router**: Uses `wouter` for client-side routing
- **State Management**: TanStack Query for server state management
- **UI Framework**: shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **Forms**: React Hook Form with Zod validation

### Backend Architecture
- **API Server**: Express.js with TypeScript
- **Database Layer**: Drizzle ORM with Neon PostgreSQL adapter
- **Authentication**: Passport.js with OpenID Connect (Replit Auth)
- **Session Storage**: PostgreSQL-backed sessions using connect-pg-simple
- **OSINT Services**: Modular service architecture for different investigation tools

### Database Schema
- **Users**: Stores user profile information from OIDC provider
- **Investigations**: Main investigation cases with metadata and progress tracking
- **Investigation Results**: Tool-specific execution results and status
- **Findings**: Individual discoveries from OSINT tools with categorization
- **Sessions**: Authentication session storage

### OSINT Tool Integration
The platform integrates multiple OSINT tools through a service-oriented architecture:
- **Maigret**: Username analysis across 3000+ platforms
- **HaveIBeenPwned**: Data breach detection for email addresses
- **Namechk**: Username availability checking across platforms
- **SpiderFoot**: Automated OSINT data collection
- **Risk Assessment**: Algorithmic risk scoring based on findings

## Data Flow

1. **Investigation Creation**: User submits investigation form with target and selected tools
2. **Async Processing**: Investigation runs asynchronously in background with progress tracking
3. **Tool Execution**: Each enabled tool runs sequentially, storing results and findings
4. **Risk Assessment**: System calculates risk score based on discovered findings
5. **Real-time Updates**: Frontend polls for status updates during investigation execution
6. **Results Display**: Comprehensive results dashboard with tool-specific views

## External Dependencies

### Core Infrastructure
- **Database**: Neon PostgreSQL serverless database
- **Authentication**: Replit OIDC provider for user authentication
- **Session Storage**: PostgreSQL-backed session management

### OSINT Tools (Optional/Fallback)
- **Maigret**: Python-based username enumeration tool (falls back to mock data)
- **HaveIBeenPwned API**: Requires API key for real breach data
- **SpiderFoot**: Python OSINT automation framework (falls back to mock data)

### Frontend Libraries
- **UI Components**: Comprehensive shadcn/ui component library
- **Icons**: Lucide React icon library
- **Charts**: Recharts for data visualization
- **Date Handling**: date-fns for date manipulation

## Deployment Strategy

### Development
- **Frontend**: Vite dev server with HMR and error overlay
- **Backend**: tsx for TypeScript execution with auto-reload
- **Database**: Drizzle Kit for schema management and migrations

### Production Build
- **Frontend**: Vite builds optimized React bundle to `dist/public`
- **Backend**: esbuild compiles TypeScript server to `dist/index.js`
- **Static Serving**: Express serves frontend build in production mode
- **Database**: Drizzle migrations applied via `db:push` command

### Environment Configuration
- **DATABASE_URL**: PostgreSQL connection string (required)
- **SESSION_SECRET**: Session encryption key (required)
- **REPL_ID**: Replit instance ID for OIDC (required in Replit environment)
- **HIBP_API_KEY**: HaveIBeenPwned API key (optional, uses mock data if missing)
- **ISSUER_URL**: OIDC issuer URL (defaults to Replit)

The application is designed to work seamlessly in the Replit environment with automatic authentication integration, while also supporting local development with appropriate environment variables.