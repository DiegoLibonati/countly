# Countly

## Educational Purpose

This project was created primarily for **educational and learning purposes**.  
While it is well-structured and could technically be used in production, it is **not intended for commercialization**.  
The main goal is to explore and demonstrate best practices, patterns, and technologies in software development.

## Description

**Countly** is a minimalist counter web application built with React 19 and TypeScript. It provides a single-page interface centered around a numeric counter that can be manipulated through three actions: **Increase** (adds 1), **Decrease** (subtracts 1), and **Reset** (returns the counter to zero).

The counter value is displayed prominently and updates in real time with each interaction. To give immediate visual feedback, the value changes color depending on its state: green when positive, red when negative, and black when exactly zero. This makes it instantly clear at a glance whether the counter is above, below, or at its baseline.

The application is fully accessible, with ARIA live regions and labeled controls so screen readers can announce every change as it happens. The layout is responsive and adapts cleanly from mobile screens to desktop viewports.

Under the hood, Countly is built on a Vite dev server with strict TypeScript settings, ESLint and Prettier enforced via a Husky pre-commit hook, and a Jest + Testing Library test suite covering rendering, interaction behavior, and color logic — all above the 70% coverage threshold.

## Technologies used

The stack reflects the tooling described above and is intentionally minimal:

1. React JS
2. TypeScript
3. Vite
4. HTML5
5. CSS3

## Libraries used

These are the exact dependencies pinned in `package.json` that power the stack listed above.

#### Dependencies

```
"react": "^19.2.4"
"react-dom": "^19.2.4"
```

#### devDependencies

```
"@eslint/js": "^9.0.0"
"@testing-library/dom": "^10.4.0"
"@testing-library/jest-dom": "^6.6.3"
"@testing-library/react": "^16.0.1"
"@testing-library/user-event": "^14.5.2"
"@types/jest": "^30.0.0"
"@types/node": "^22.0.0"
"@types/react": "^19.2.14"
"@types/react-dom": "^19.2.3"
"@vitejs/plugin-react": "^5.0.2"
"eslint": "^9.0.0"
"eslint-config-prettier": "^9.0.0"
"eslint-plugin-prettier": "^5.5.5"
"eslint-plugin-react-hooks": "^5.0.0"
"eslint-plugin-react-refresh": "^0.4.0"
"globals": "^15.0.0"
"husky": "^9.0.0"
"jest": "^30.3.0"
"jest-environment-jsdom": "^30.3.0"
"lint-staged": "^15.0.0"
"prettier": "^3.0.0"
"ts-jest": "^29.4.6"
"typescript": "^5.2.2"
"typescript-eslint": "^8.0.0"
"vite": "^7.1.6"
```

## Getting Started

Requires **Node.js >= 22**. Use `.nvmrc` with `nvm use` to switch automatically.

With the dependencies above declared in `package.json`, the local setup is straightforward:

1. Clone the repository
2. Navigate to the project folder
3. Execute: `npm install`
4. Execute: `npm run dev`

The application will open automatically at `http://localhost:3000`.

## Testing

Once the app is running locally, you can validate behavior with the Jest + Testing Library suite:

1. Navigate to the project folder
2. Execute: `npm test`

For coverage report:

```bash
npm run test:coverage
```

Coverage is enforced at a 70% threshold across rendering, interaction, and color-logic tests.

## Continuous Integration

The repository ships with a **GitHub Actions** pipeline defined in [`.github/workflows/ci.yml`](.github/workflows/ci.yml). It runs automatically on every `push` and `pull_request` targeting the `main` branch.

### Pipeline overview

```
                      ┌─── PR or push to main ───┐
                      ▼                          ▼
┌──────────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│    lint-and-audit    │─▶│      testing     │─▶│       build      │
│ eslint · tsc --noEmit│  │ jest (jsdom, 70%)│  │ tsc + vite build │
└──────────────────────┘  └──────────────────┘  └──────────────────┘
```

### Validation jobs (run on every PR and push)

1. **`lint-and-audit`** — runs `npm run lint` (ESLint on `src/`) followed by `npm run type-check` (`tsc -p tsconfig.app.json --noEmit`).
2. **`testing`** — runs `npm run test` (Jest + Testing Library on `jsdom`, 70% coverage threshold enforced). Depends on `lint-and-audit`.
3. **`build`** — runs `npm run build` (type-check + Vite production build) as a smoke test that the bundle compiles. Depends on `testing`.

Each stage depends on the previous one, so the build only runs if lint, type-check and tests pass. All jobs run on `ubuntu-latest`, pin Node.js to the version declared in [`.nvmrc`](.nvmrc) via `actions/setup-node`, and reuse the npm cache between runs.

### Where the build outputs live

| Output                                    | Location                     |
| ----------------------------------------- | ---------------------------- |
| Validation logs (lint, type-check, tests) | **Actions** tab on GitHub    |
| Production bundle (`dist/`)               | Ephemeral, inside the runner |

> **Note:** This pipeline is validation-only — it does not publish releases, tags, or artifacts. The production bundle is rebuilt locally with `npm run build` when needed.

### Running the same checks locally

```bash
# lint-and-audit
npm run lint
npm run type-check

# testing
npm run test

# build
npm run build
```

## Security Audit

Beyond functional tests, you can also audit dependencies and overall project health.

### npm audit

Check for vulnerabilities in dependencies:

```bash
npm audit
```

### React Doctor

Run a health check on the project (security, performance, dead code, architecture):

```bash
npm run doctor
```

Use `--verbose` to see specific files and line numbers:

```bash
npm run doctor -- --verbose
```

## Known Issues

None at the moment.

## Portfolio Link

[`https://www.diegolibonati.com.ar/#/project/countly`](https://www.diegolibonati.com.ar/#/project/countly)
