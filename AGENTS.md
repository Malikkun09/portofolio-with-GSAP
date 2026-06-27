# AGENTS.md

## Cursor Cloud specific instructions

### Repository layout
- The **primary product** is the root project: a static **React 19 + Vite + TypeScript + Tailwind** single-page portfolio (`malikfajar-portfolio`). It is frontend-only — there is no backend, API, database, or environment variables/secrets (`DESIGN.md` explicitly forbids backend code). Contact info is base64-obfuscated client-side in `src/lib/secure-contact.ts`.
- `loading screen/` is a **separate, unused** Next.js 16 + Bun + Prisma/SQLite prototype. It is NOT imported by the portfolio and is not needed to run or test it. The startup VM update script does not install its deps (it uses Bun, not npm). Only touch it if a task specifically targets it; if so, set it up manually (`bun install`, `DATABASE_URL="file:./db/custom.db"`, `bun run db:push`, `bun run dev`).

### Running the portfolio (root project)
- Dev server: `npm run dev` → http://localhost:3000 (port set in `vite.config.ts`).
- Build: `npm run build` (`tsc -b && vite build`, outputs to `dist/`).
- Preview built output: `npm run preview`.
- Standard scripts live in `package.json`; deployment config in `vercel.json`.

### Gotchas
- **`npm run lint` is broken out of the box.** The script runs `eslint .`, but `eslint` is not declared as a dependency and there is no ESLint config in the repo, so it fails with `eslint: not found`. Treat lint as unavailable unless ESLint + a config are added.
- The **Skills / "Tech Stack" section is scroll-driven** (GSAP "trace the circuit" reveal). Its content reveals as you scroll through it; jumping straight to it via a nav link can show it blank/black until you scroll. This is animation behavior, not a crash.
