# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is **Astro Nano**, a static, minimalist portfolio and blog built with Astro 5, TypeScript, and Tailwind CSS. The site is deployed to GitHub Pages at https://707.github.io and focuses on performance, accessibility, and minimal design.

## Development Commands

| Command                   | Purpose                                           |
| :------------------------ | :----------------------------------------------- |
| `npm run dev`             | Start dev server at `localhost:4321`             |
| `npm run dev:network`     | Start dev server on local network                |
| `npm run build`           | Build production site (includes `astro check`)   |
| `npm run preview`         | Preview build locally                            |
| `npm run preview:network` | Preview build on local network                   |
| `npm run lint`            | Run ESLint                                       |
| `npm run lint:fix`        | Auto-fix ESLint issues                          |

**Important**: The build command runs `astro check` for type checking before building. Always run this before deploying.

## Architecture & Content Structure

### Content Collections (src/content/)

The site uses Astro's content collections with strict schemas:

- **blog/**: Blog posts with `title`, `description`, `date`, and optional `draft` field
- **work/**: Work experience with `company`, `role`, `dateStart`, `dateEnd` 
- **projects/**: Portfolio projects with `title`, `description`, `date`, optional `draft`, `demoURL`, `repoURL`

### Site Configuration (src/consts.ts)

Central configuration for:
- Site metadata (name, email, homepage post/work/project counts)
- Social links (GitHub, LinkedIn)
- Page-specific metadata (titles, descriptions)

### Key Directories

- **src/components/**: Reusable Astro components (Header, Footer, ArrowCard, etc.)
- **src/layouts/**: Page layouts (currently just PageLayout.astro)
- **src/pages/**: Route pages including dynamic routes for content collections
- **src/lib/**: Utility functions
- **src/styles/**: Global CSS styles

### Design System

- Uses Tailwind CSS with custom font configuration (Inter + Lora)
- Built-in dark mode support via `class` strategy
- Typography plugin for markdown content styling
- Minimal, clean aesthetic focused on readability

## Deployment

- Automatically deploys to GitHub Pages via GitHub Actions on main branch pushes
- Uses `pnpm` as the package manager
- Node.js 20 runtime in CI/CD

## Development Notes

- All content is in Markdown/MDX format with frontmatter schemas
- Static site generation with no client-side frameworks
- RSS feed auto-generated at `/rss.xml`
- Sitemap auto-generated
- TypeScript strict mode enabled
- Path aliases configured (`@components`, `@types`, etc.)