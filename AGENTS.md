# Repository Guidelines

## Project Structure & Module Organization
Open WebUI pairs a Svelte front end with a Python backend. Front-end source lives in `src/` (routes, `lib/` modules, component-specific stores) with static assets in `static/`. Backend service code sits in `backend/open_webui/` and is bootstrapped through `backend/start.sh`. API data files and migrations stay under `backend/data/`. End-to-end artefacts reside in `cypress/`, while fixture content for automated runs is under `test/test_files/`. Documentation and deployment assets are grouped in `docs/`, `docker-compose*.yaml`, and `kubernetes/`.

## Build, Test, and Development Commands
Run `npm install` followed by `npm run dev` to launch the Svelte dev server on your host; use `npm run dev:5050` when you need a fixed port. `npm run build` performs a production Vite build after fetching Pyodide bundles, and `npm run preview` serves the compiled output. Start the Python API locally with `./backend/start.sh --reload`. For container workflows, `make install` brings up the compose stack and `make stop` tears it down.

## Coding Style & Naming Conventions
TypeScript, Svelte, and styles are formatted with Prettier (2-space indentation) and linted via ESLint + `svelte-check`. Prefer PascalCase for Svelte components (`ChatPanel.svelte`) and camelCase for utilities inside `src/lib`. Backend modules should follow snake_case filenames and comply with Black’s defaults plus `pylint` warnings. Run `npm run format` or `npm run format:backend` before submitting.

## Testing Guidelines
Unit-level UI specs use Vitest; run `npm run test:frontend` and keep specs beside the code in `src`. End-to-end flows live in `cypress/e2e`; open the runner with `npm run cy:open` or run headless through `npx cypress run`. Backend additions should include pytest coverage (mirroring the path under `backend/open_webui/tests` if created) and keep shared fixtures under `test/test_files`. Failing tests block merges, so run checks locally before pushing.

## Commit & Pull Request Guidelines
Follow the conventional commit style already in use (`feat:`, `fix:`, `chore:`). Each commit should address a focused concern and include relevant migrations or assets. PRs need a concise summary, reproduction or verification notes, linked issues, and screenshots or curl examples for UI/API changes. Confirm that `npm run lint`, `npm run check`, and backend linters pass, and flag any migrations or manual steps in the description.

## Security & Configuration Tips
Secrets are loaded by `backend/start.sh`; never commit generated keys or `.env` files. Prefer `.env.example` updates when introducing settings, and document any new ports or scopes under `docs/`.
