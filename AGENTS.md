## Cursor Cloud specific instructions

### Project overview

companion-caspar-configurator is a Node.js/TypeScript CLI tool that creates buttons in Bitfocus Companion for playing videos from a CasparCG server. It uses `ts-node` for direct TypeScript execution.

### Development commands

- **Install deps:** `npm ci`
- **Lint:** `npm run lint` (runs prettier then eslint)
- **Build:** `npm run build` (runs `tsc`)
- **Test:** `npm run test` (lint + build)
- **Start:** `npm start` (runs `ts-node --files --project tsconfig.json src/index.ts`)

### Known issues

- `npm run lint:eslint` fails with a pre-existing compatibility issue: the `@gamesdonequick/eslint-config` shared config uses an `accessor-pairs` rule option (`enforceForClassMembers`) not supported by the pinned ESLint 6.3.0. Prettier lint (`npm run lint:prettier`) and the TypeScript build both pass cleanly.
- Use `npm ci` (not `npm install`) to avoid reformatting `package-lock.json`, which would cause prettier lint failures.

### Running the application

The app requires a `ruleset.ts` file in the project root (see README for the format). It also needs connections to a CasparCG server (default `127.0.0.1:5250`) and Bitfocus Companion (default `127.0.0.1:8000`). Without these external services, the app starts but logs connection warnings. A `config.json` can override default connection settings.

### Git hooks

Husky is configured with `commit-msg` (commitlint with conventional commits) and `pre-commit` (lint-staged with prettier + eslint auto-fix). These hooks are defined in `package.json` under `"husky"` and `"lint-staged"`.
