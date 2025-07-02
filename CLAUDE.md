# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

Use pnpm as the package manager:

- `pnpm dev` - Start development server
- `pnpm build` - Build for production
- `pnpm start` - Start production server
- `pnpm lint` - Run ESLint
- `pnpm lint:fix` - Fix linting issues automatically

## Payload CMS Commands

- `pnpm payload` - Access Payload CLI
- `pnpm generate:types` - Generate TypeScript types from Payload config
- `pnpm generate:importmap` - Generate import map for admin panel

## Database Commands (Postgres)

- `pnpm payload migrate:create` - Create a new migration (local development)
- `pnpm payload migrate` - Run pending migrations (production)

## Architecture Overview

This is a Payload CMS website template built with Next.js 15 and TypeScript. The application combines a headless CMS backend with a production-ready frontend in a single deployment.

### Core Stack
- **Backend**: Payload CMS 3.40.0 with PostgreSQL adapter
- **Frontend**: Next.js 15.3.0 with App Router
- **Styling**: TailwindCSS with shadcn/ui components
- **Database**: PostgreSQL
- **Forms**: React Hook Form
- **Rich Text**: Lexical editor

### Key Directory Structure

- `src/collections/` - Payload CMS collections (Pages, Posts, Media, Categories, Users)
- `src/globals/` - Global data structures (Header, Footer)
- `src/blocks/` - Reusable content blocks for layout builder
- `src/app/(frontend)/` - Next.js frontend pages and routes
- `src/app/(payload)/` - Payload admin panel and API routes
- `src/components/` - Shared React components
- `src/utilities/` - Helper functions and utilities

### Content Architecture

The CMS uses a layout builder pattern with reusable blocks:
- **Collections**: Pages, Posts, Media, Categories, Users
- **Blocks**: Hero, Content, Media, CallToAction, Archive, Banner, Code, Form
- **Globals**: Header and Footer configuration

### Access Control

- **Users**: Admin access to CMS and unpublished content
- **Posts/Pages**: Public access to published content, user access for CRUD operations
- Uses draft/published workflow with preview functionality

### Key Features

- Layout builder with reusable blocks
- Draft preview and live preview
- On-demand revalidation for static generation
- SEO plugin integration
- Search functionality
- Redirects management
- Form builder
- Scheduled publishing with job queue

### Environment Setup

Requires `.env` file with:
- `DATABASE_URI` - PostgreSQL connection string
- `PAYLOAD_SECRET` - Secret key for Payload
- `CRON_SECRET` - For scheduled jobs (Vercel deployment)

### Development Notes

- Uses PostgreSQL with `push: true` in development for schema flexibility
- Migrations required for production deployments
- Static generation with ISR (Incremental Static Regeneration)
- Docker support available via docker-compose.yml