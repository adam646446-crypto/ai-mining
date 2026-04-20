# AI Mining Platform

## Overview

Full-stack AI Mining Platform — a premium, futuristic web application where users earn passive income through AI-powered mining machines. Features a dark glassmorphism theme with gold and electric blue accents, mining machine store, 3-level referral system, and wallet management.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite (Tailwind CSS v4, shadcn/ui, Orbitron/Inter fonts)
- **Backend**: Express 5 (API server)
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Routing**: wouter (frontend)
- **State management**: React Query (TanStack)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

## Architecture

### Frontend (artifacts/ai-mining-platform/)
- `/` — Landing + Auth page with animated circuit board background
- `/dashboard` — Main dashboard: hero, top miners, my machines, live stats, machine store, referral system, footer
- `/wallet` — Wallet management with deposit functionality

### Backend (artifacts/api-server/)
Routes:
- `GET /api/users/me` — get current user (requires X-User-Uid header)
- `PUT /api/users/me` — update user profile
- `POST /api/users/register` — register/sync Firebase user
- `POST /api/users/wallet/deposit` — add funds to wallet
- `GET /api/machines` — list available mining machines
- `POST /api/machines/purchase` — purchase a machine
- `GET /api/machines/my` — get user's active machines
- `GET /api/referral/info` — referral stats and team info
- `GET /api/referral/team` — referral team members by level
- `GET /api/stats/platform` — platform-wide statistics
- `GET /api/stats/top-miners` — top 5 miners of the day

### Database (lib/db/)
Tables:
- `users` — user accounts with referral codes
- `machines` — available mining machines catalog
- `user_machines` — purchased machines per user
- `commission_history` — referral commission records

## Auth System
- Mock auth using localStorage (ready for Firebase integration)
- Auth context stores uid/name/email and injects X-User-Uid header into all API calls via `setUserUid()` from api-client-react

## Mining Machines
- AI Miner Basic: $10, $0.50/day, 40 days
- AI Miner Pro: $30, $1.80/day, 40 days (HOT)
- AI Miner Elite: $100, $7.00/day, 40 days
- AI Miner Titan: $300, $22.00/day, 40 days (BEST VALUE)
- AI Miner Ultra: $500, $40.00/day, 40 days
- AI Miner Quantum: $1000, $90.00/day, 40 days (HOT)

## Referral System
- 3-level commission structure: L1=10%, L2=5%, L3=2%
- Commissions stored in `commission_history` table
- Team viewer with accordion by level

## Theme
- Background: #0A0A0F / #0D1117
- Primary accent: Gold #F5C518
- Secondary accent: Electric blue #00D4FF
- Purple gradient atmosphere
- Glassmorphism cards (backdrop-blur + semi-transparent + border glow)
- Fonts: Orbitron (headings) + Inter (body)
