## Cursor Cloud specific instructions

### Project overview

companion-caspar-configurator is a Node.js/TypeScript CLI tool that creates buttons in Bitfocus Companion for playing videos from a CasparCG server. It uses `ts-node` for direct TypeScript execution.

### Development commands

- **Install deps:** `npm ci`
- **Lint:** `npm run lint` (runs Biome format check, then ESLint)
- **Build:** `npm run build` (runs `tsc`)
- **Test:** `npm run test` (lint + build)
- **Start:** `npm start` (runs `ts-node --files --project tsconfig.json src/index.ts`)
- **Format (write):** `npm run fix:biome` (applies [Biome](https://biomejs.dev/) to TS/JS/JSON/HTML covered by `biome.json`)

### Formatting note (Ruff vs Biome)

[Ruff](https://github.com/astral-sh/ruff) from Astral is an excellent linter/formatter, but it targets **Python** only. This repository is **TypeScript** with no Python sources, so Ruff cannot replace a JS/TS formatter. We use **[Biome](https://biomejs.dev/)** instead: a fast formatter (and optional linter) with a single binary, similar goals for the web stack. Markdown and YAML are not auto-formatted in CI (Biome does not fully replace Prettier for those yet); edit them by hand or run another tool locally if needed.

### Known issues

- `npm run lint:eslint` fails with a pre-existing compatibility issue: the `@gamesdonequick/eslint-config` shared config uses an `accessor-pairs` rule option (`enforceForClassMembers`) not supported by the pinned ESLint 6.3.0. Biome format check (`npm run lint:biome`) and the TypeScript build both pass cleanly.
- Prefer `npm ci` for reproducible installs. If you run `npm install`, re-run `npm run fix:biome` before committing when Biome reformats `package.json` or other included files.

### Running the application

The app requires a `ruleset.ts` file in the project root (see README for the format). It also needs connections to a CasparCG server (default `127.0.0.1:5250`) and Bitfocus Companion (default `127.0.0.1:8000`). Without these external services, the app starts but logs connection warnings. A `config.json` can override default connection settings.

### Git hooks

Husky is configured with `commit-msg` (commitlint with conventional commits) and `pre-commit` (lint-staged with Biome format + ESLint auto-fix). These hooks are defined in `package.json` under `"husky"` and `"lint-staged"`.
