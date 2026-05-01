# AGENTS Guide

This repository is an OpenCode configuration and agent/skill workspace.
Most files are Markdown instructions with YAML frontmatter, plus a few Node and Bash utility scripts.

Use this file as the default guide for agents working anywhere in the repo.
If a deeper directory contains its own `AGENTS.md`, follow the more specific file there.

## Repository Shape

- Root `package.json` is minimal and only declares `@opencode-ai/plugin`.
- `agents/` contains agent definition Markdown files.
- `.agents/skills/` contains skill definitions, generated guides, and helper scripts.
- `skills/` contains installed skill content mirrored for OpenCode use.
- The only concrete code in this repo lives primarily in:
- `.agents/skills/brainstorming/scripts/`
- `.agents/skills/nestjs-best-practices/scripts/`

## Cursor And Copilot Rules

- No `.cursorrules` file exists in this repo.
- No `.cursor/rules/` directory exists in this repo.
- No `.github/copilot-instructions.md` file exists in this repo.
- Do not claim any Cursor or Copilot rules exist unless they are added later.

## Tooling Reality

- Root package manager appears to be Bun because `bun.lock` exists.
- The root `package.json` has no `scripts` section.
- There is no repo-level ESLint, Prettier, Biome, Jest, or Vitest config.
- There is no repo-level `tsconfig.json`.
- There are no real repo-level test files or test runner configs today.

## Root Commands

Run from the repo root only when needed:

```sh
bun install
```

Important constraints:

- There is no root `build` command.
- There is no root `lint` command.
- There is no root `test` command.
- There is no root single-test command because no repo-level test framework is configured.

## Real Subproject Commands

The only defined npm scripts are in `.agents/skills/nestjs-best-practices/scripts/package.json`.

Run from `.agents/skills/nestjs-best-practices/scripts`:

```sh
npm install
npm run build
npm run build:watch
```

Meaning:

- `npm run build` runs `npx ts-node build-agents.ts`.
- `npm run build:watch` watches `../rules/*.md` and regenerates that skill's `AGENTS.md`.
- The nearest thing to a focused single-target command in this repo is `npx ts-node build-agents.ts` in that same directory.

## Test Guidance

- No repo-level automated tests are configured.
- No repo-level single-test command exists.
- `jest` and `supertest` references in skill docs are example content only, not runnable tests in this workspace.
- Do not invent `npm test`, `bun test`, `vitest`, or `jest` commands unless the user adds a real test setup.

## Practical Validation Commands

These are ad hoc checks, not official project scripts:

```sh
node --check ".agents/skills/brainstorming/scripts/helper.js"
node --check ".agents/skills/brainstorming/scripts/server.cjs"
bash -n ".agents/skills/brainstorming/scripts/start-server.sh"
bash -n ".agents/skills/brainstorming/scripts/stop-server.sh"
```

For NestJS skill generation changes, prefer:

```sh
npm run build
```

from `.agents/skills/nestjs-best-practices/scripts`.

## Editing Priorities

- Keep changes minimal and local.
- Preserve existing file layout, naming, and tone.
- Avoid introducing new tooling or dependencies unless the task truly requires it.
- Do not broad-refactor Markdown-heavy areas unless the user asked for that.
- Check whether a file is generated before editing it directly.

## Markdown And Frontmatter

- Many important files are Markdown documents with YAML frontmatter.
- Preserve frontmatter blocks exactly unless the task is specifically to change metadata.
- Keep frontmatter keys lowercase unless the surrounding file uses another style.
- Do not reorder frontmatter fields without a reason.
- Keep prose direct, operational, and optimized for agents.
- Prefer explicit rules and concrete examples over long narrative explanations.
    
## JavaScript And TypeScript Style

- Follow the surrounding file before imposing a new style.
- Use 2-space indentation.
- Use semicolons.
- Use single quotes.
- Prefer `const` by default and `let` only when mutation is required.
- Prefer top-level `function` declarations for reusable helpers.
- Use early returns for guard conditions.
- Keep helpers small and purpose-specific.
- Avoid clever abstractions in one-off scripts.

## Module, Naming, And Types

- `.cjs` files use CommonJS with `require(...)`.
- `.ts` build scripts use ESM-style `import` syntax.
- Do not switch module systems unless there is a concrete need.
- Use `camelCase` for variables and functions.
- Use `PascalCase` for interfaces and type-like constructs.
- Use `UPPER_SNAKE_CASE` for protocol constants and env-style values.
- Keep filenames stable and kebab-case where that pattern already exists.
- Add types where the file already uses TypeScript.
- Prefer explicit interfaces for structured parsed data and metadata.
- Keep imports simple and readable.
- Match local conventions for built-in Node imports, such as `import * as fs from 'fs';` in TypeScript scripts.
- Do not migrate JavaScript files to TypeScript without a strong reason.

## Error Handling

- Fail fast on invalid CLI arguments and missing prerequisites.
- Handle JSON parsing, socket boundaries, and filesystem reads explicitly.
- Prefer clear, actionable error messages.
- Use `try`/`catch` at parsing and transport boundaries.
- Use early returns after recoverable failures.
- Preserve existing machine-readable output contracts, especially JSON status messages from scripts.

## Shell Script Conventions

- Quote variable expansions.
- Prefer `[[ ... ]]` tests in Bash.
- Keep environment variable names uppercase.
- Keep command-line parsing explicit with `case` blocks.
- Preserve cleanup behavior and platform guards already present in the script.

## Generated Content

- `.agents/skills/nestjs-best-practices/AGENTS.md` is generated by `build-agents.ts`.
- Prefer editing source rule files or metadata instead of hand-editing generated output.
- If you change generation logic or rule content there, run `npm run build` in the scripts subdirectory.

## Validation And Safety

- Run the smallest relevant validation first.
- Prefer file-targeted syntax checks over broad command guessing.
- If no real automated validation exists, say so plainly.
- Do not claim tests passed if you only ran syntax checks or generation commands.
- Expect a dirty worktree and never revert unrelated user changes.
- Do not delete generated files unless the task requires regeneration or cleanup.
