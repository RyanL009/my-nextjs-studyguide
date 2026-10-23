> ### 🚧 PROJECT STATUS: ACTIVE ARCHITECTURAL PROPOSAL / WIP
> **Current Phase:** Core Plumbing & Engine Validation (Step 1-2 + Synthesized Realtime Module)  
> *Notice: This codebase is an active work in progress and serves as a living study tool. The internal directory naming conventions, feature modularity boundaries, and data routing structures are experimental and intentionally not set in stone. Expect frequent structural adjustments over the next 2-3 weeks as advanced Next.js caching rules and database handshakes are actively tested and validated.*

---

# 🎓 Next.js 15+ & Supabase Living Study Guide

A highly structured **Next.js 15+ (App Router)** application built with **TypeScript**, **Tailwind CSS**, and **Postgres via Supabase**. 

Instead of being a traditional consumer application, the sole purpose of this project is to serve as a **practical, living study guide**. The application features an interactive top-navigation dashboard layout designed to visually demonstrate framework rendering lifecycles, caching behaviors, and client-server database architectures side-by-side using real-time components, technical text explanations, and raw code reference snippets built right into the interface.

---

## 🚀 Optimized UX Strategy: SSR + Stream Ground Zero
To best observe rendering architecture the instant the application opens, the root path (`/`) features an instant, server-level redirect that drops the user directly into our flagship **Unified SSR + WebSocket Stream Showcase**. 

This page synthesizes raw **Server-Side Rendering (SSR)** with persistent **WebSockets**. The initial data payload loads instantly on the server side to eliminate component flash, while an active background WebSocket channel catches database adjustments pushed down by an automated server task every 10 minutes. A manual client-side override button allows users to force a fresh Next.js server network cycle on-demand.

---

## 🏗️ Proposed Architectural Pattern: Domain/Feature-Driven (Modular)
This project currently experiments with an industry-standard **Modular Feature Structure** (Option B). All components, interactive views, style primitives, and database mutation hooks are grouped tightly within self-contained business domains inside the `features/` directory. This keeps our routing pages entirely decoupled from layout-specific logic.

### 📂 Repository File Structure Blueprint
```text
my-nextjs-studyguide-practical/
├── src/
│   ├── app/                      # Next.js App Router (Routing Layers Only)
│   │   ├── page.tsx              # Server Redirect: "/" ──> "/concepts/unified-ssr-stream"
│   │   └── concepts/
│   │       ├── page.tsx          # Server Redirect: "/concepts" ──> "/concepts/unified-ssr-stream"
│   │       ├── layout.tsx        # Persistent Header & Tab orchestration shell
│   │       └── unified-ssr-stream/ # Consolidated Module Route: SSR + Live WebSocket Hybrid
│   │           └── page.tsx      
│   ├── features/                 # Self-contained business modules
│   │   └── rendering-dashboard/  # The Core Concepts Module Workspace
│   │       └── components/       
│   │           ├── ConceptTabs.tsx      # Client tab controller (manages active paths)
│   │           └── UnifiedShowcase.tsx  # Component: Hybrid SSR view, socket listeners, and code
│   ├── lib/                      # Central Shared Infrastructure
│   │   └── supabase/             
│   │       ├── client.ts         # Browser-Side DB Client ("use client" WebSockets)
│   │       └── server.ts         # Secure Cloud-Side DB Client (Handles layout cookies)
│   └── types/
│       └── supabase.ts           # Database column definitions pulled from Postgres schema
├── public/                       # Static public assets
├── .env.local                    # Secret environmental endpoint keys
├── pnpm-lock.yaml                # Rigid pnpm package state locker
├── package.json                  # Application configurations and script maps
├── tailwind.config.ts            # Tailwind CSS configuration maps
└── README.md                     # The repository master manual
```

---

## 🧱 Proposed Core Concepts Roadmap

The top-navigation bar layout sets a distinct rendering configuration connecting to your Supabase Postgres database. While the project launches directly into the **Unified Hybrid Showcase**, it is structured to scale smoothly across the remaining cached pillars as the proposal solidifies:

1. **⚡ Synthesized SSR + Live WebSocket Stream [ACTIVE GROUND ZERO]**
   * **Next.js Engine Config:** `export const dynamic = 'force-dynamic'` + `router.refresh()`
   * **Mechanism:** Renders the initial layout on the server to prevent loading states, then maintains an active browser WebSocket channel. A background database timer (`pg_cron`) modifies metrics every 10 minutes, pushing changes to the UI without page updates. A manual client-side button invokes a server-rendered component refresh to demonstrate on-demand SSR.

2. **📦 Static Site Generation (SSG) [LOCKED PROPOSAL TEMPLATE]**
   * **Next.js Engine Config:** `cache: 'force-cache'`
   * **Mechanism:** Fetches data once at build time. The layout timestamp remains completely frozen across refreshes, showcasing optimized edge-cached responses.

3. **🕒 Time-Based Revalidation (ISR) [LOCKED PROPOSAL TEMPLATE]**
   * **Next.js Engine Config:** `{ next: { revalidate: 10 } }`
   * **Mechanism:** A hybrid approach that serves cached assets instantly, but quietly purges and re-compiles data at most once every 10 seconds asynchronously in the background.

4. **🚀 On-Demand Revalidation [LOCKED PROPOSAL TEMPLATE]**
   * **Next.js Engine Config:** `{ next: { tags: ['study-guide-data'] } }` + `revalidateTag()`
   * **Mechanism:** Statically caches database rows indefinitely until a custom Server Action form is submitted, instantly clearing the framework cache block on-demand.

---

## 🛠️ Step-by-Step Implementation Phase

### Step 1: Foundations & Supabase Plumbing ⚙️
1. Set up the local Git workspace and install packages (`@supabase/ssr`, `@supabase/supabase-js`, `typescript`, `tailwindcss`).
2. Add environment parameters to `.env.local` to securely hook up database endpoints.
3. Configure `src/lib/supabase/server.ts` and `client.ts` to manage both server cookie stores and client browser real-time events.
4. Execute migration strings via the Supabase SQL tool and run `npx supabase gen types` to produce structural data schemas.

### Step 2: Hybrid Showcase Compilation 🟩
1. Construct the modular scopes inside `features/rendering-dashboard/components/`.
2. Implement `ConceptTabs.tsx` using Next.js’s `"use client"` `usePathname()` hook to cleanly map URL paths to highlighted active buttons.
3. Build out `UnifiedShowcase.tsx` initializing the browser WebSocket stream alongside a `useTransition` block mapped to `router.refresh()`.
4. Deploy the cloud data container `app/concepts/unified-ssr-stream/page.tsx` to handle secure initial row extractions.

---

## 🏁 Quick Start Setup Commands

```bash
# 1. Install framework core and database ecosystem packages
pnpm add @supabase/ssr @supabase/supabase-js
pnpm install

# 2. Synchronize your database types from your active Supabase cloud layer
pnpm exec supabase gen types typescript --project-id "your-project-id" > src/types/supabase.ts

# 3. Spin up the local development compiler
pnpm dev
```
