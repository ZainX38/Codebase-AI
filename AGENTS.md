# Repository Guidelines

## Project Structure & Module Organization

AI-Codebase is an early-stage application for connecting GitHub repositories and eventually answering questions about their code. AI question answering is not implemented yet.

- `frontend/app/`: Next.js pages, global styles, and shared UI in `components/`.
- `frontend/lib/`: API requests and Auth0 setup; `frontend/proxy.ts` handles authentication routing.
- `frontend/public/`: static assets, including the application logo.
- `backend/main.py`: FastAPI endpoints and GitHub/Auth0 integration.
- `backend/pyproject.toml` and `backend/uv.lock`: Python dependencies and lockfile.

No dedicated test directory currently exists.

## Next.js

<!-- BEGIN:nextjs-agent-rules -->
 
# This is NOT the Next.js you know
 
This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `frontend/node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.
 
This block is written and re-added by `next dev` — verify at `frontend/node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.
 
<!-- END:nextjs-agent-rules -->

## Build, Test, and Development Commands

Run frontend commands from `frontend/`:

- `npm ci`: install dependencies from the lockfile.
- `npm run dev`: start the development server on port 3000.
- `npm run lint`: run ESLint with Next.js and TypeScript rules.
- `npm run build`: create a production build.
- `npm start`: serve the production build after building.

From `backend/`, use Python 3.14 or newer:

- `uv sync`: install locked dependencies.
- `uv run --env-file .env fastapi dev main.py`: start the API on port 8000 with local configuration.

## Coding Style & Naming Conventions

Match surrounding formatting; existing TypeScript indentation varies between two and four spaces. Use four spaces for Python. Prefer PascalCase React component names, camelCase TypeScript functions and variables, and snake_case Python functions and variables. Keep Next.js route filenames such as `page.tsx` and `layout.tsx`. Use `@/` imports for frontend-local modules. TypeScript strict mode is enabled; prefer explicit types over new `any` usage. No standalone formatter is configured.

## Testing Guidelines

No automated test framework, test script, or coverage threshold is configured. For changes, run frontend lint and build checks and manually verify affected flows, including sign-in, repository submission, and error handling. Document results and configuration blockers. If adding tests, establish and document their runner, location, and naming convention.

## Commit & Pull Request Guidelines

History uses descriptive, free-form messages such as “Added proxy for authentication”; no consistent Conventional Commits requirement exists. Keep commits focused and describe the behavior changed. PRs should explain purpose, summarize changes, list validation, link relevant issues, and include screenshots for UI changes.

## Security & Configuration

Keep credentials in ignored environment files. The backend requires `AUTH0_DOMAIN`, `AUTH0_CLIENT_ID`, and `AUTH0_CLIENT_SECRET`; the frontend supports `NEXT_PUBLIC_BACKEND_URL`. Never commit or log tokens or session secrets. Backend repository state is currently temporary and shared; account for user isolation when extending it.