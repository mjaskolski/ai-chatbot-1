# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Essential Commands
- `pnpm dev` - Start development server with Turbo
- `pnpm build` - Run DB migrations and build for production
- `pnpm lint` - Run Next.js lint and Biome lint with auto-fix
- `pnpm format` - Format code with Biome
- `pnpm test` - Run Playwright E2E tests

### Database Commands
- `pnpm db:generate` - Generate Drizzle migrations from schema
- `pnpm db:migrate` - Apply pending migrations
- `pnpm db:studio` - Open Drizzle Studio for database exploration
- `pnpm db:push` - Push schema changes directly (dev only)

### Testing
Tests are written in Playwright and located in `/tests`:
- E2E tests: `/tests/e2e/*.test.ts`
- Route tests: `/tests/routes/*.test.ts`
- Run specific test: `pnpm exec playwright test path/to/test.ts`
- Test timeout: 240 seconds (configured in playwright.config.ts)

## Architecture Overview

This is a Next.js 15 AI chatbot application using:
- **React 19.0.0-rc** with App Router
- **AI SDK v5** (beta) with xAI (Grok models) as default provider
- **PostgreSQL** via Drizzle ORM (Vercel Postgres/Neon)
- **Auth.js v5** for authentication
- **Vercel Blob** for file storage
- **Redis** for streaming/caching

### Key Directories

- `/app` - Next.js App Router pages and API routes
  - `/(auth)` - Login/register pages
  - `/(chat)` - Main chat interface
  - `/api` - API endpoints for chat, documents, files
  
- `/components` - React components
  - UI components use shadcn/ui (Radix UI based)
  - Chat-specific components (messages, input, artifacts)
  
- `/lib` - Core business logic
  - `/ai` - AI provider configuration and tools
  - `/db` - Database schema and queries (Drizzle)
  - `/editor` - Text editor configurations
  - `/artifacts` - Artifact system logic

- `/artifacts` - Artifact handling system
  - Support for code, text, image, and spreadsheet artifacts
  - Each type has client and server components

### Database Schema

Main tables in `lib/db/schema.ts`:
- `User` - User accounts
- `Chat` - Chat sessions with visibility settings
- `Message_v2` - Messages with parts and attachments
- `Vote_v2` - Message voting system
- `Document` - Document storage

### AI Provider Configuration

Located in `lib/ai/providers.ts`:
- Chat model: `grok-2-vision-1212`
- Reasoning model: `grok-3-mini-beta` (with reasoning middleware)
- Title/Artifact model: `grok-2-1212`
- Image model: `grok-2-image`

### Code Style

- **Biome** for linting and formatting (config in `biome.jsonc`)
- 2 spaces indentation
- Single quotes for JS/TS, double quotes for JSX
- Semicolons required
- Trailing commas in multiline expressions

### Environment Variables

Required variables (see `.env.example`):
- `POSTGRES_URL` - PostgreSQL connection string
- `NEXT_PUBLIC_APP_URL` - Application URL
- `AUTH_SECRET` - Auth.js secret
- `XAI_API_KEY` - xAI API key
- `BLOB_READ_WRITE_TOKEN` - Vercel Blob storage token

### Important Patterns

1. **Server Components by Default** - Use `'use client'` only when needed
2. **Streaming Responses** - Chat uses AI SDK streaming with Redis support
3. **Artifact System** - Creates editable content within chats
4. **Public/Private Chats** - Visibility controlled via `visibility` field
5. **Tool Integration** - Weather tool example in `lib/ai/tools`

### Testing Approach

- Playwright for E2E testing
- Tests use fixtures in `/tests/fixtures`
- Helper utilities in `/tests/test-utils.ts`
- Mock AI models available for testing (`lib/ai/models.test.ts`)