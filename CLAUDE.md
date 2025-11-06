# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## ⚠️ Template Setup Required

**This is currently a template repository.** If you see this message, you need to set up a new project by updating the following:

1. **Package names**: Update `@ascorbic/example` in all `package.json` files to your new package name
2. **Repository URLs**: Update git repository URLs in `package.json` files
3. **README files**: Update README.md files with your project information
4. **Test files**: Rename `packages/example/test/hello.test.ts` to a more appropriate test name
5. **Package directory**: Rename `packages/example/` to your actual package name
6. **Workspace name**: Update the workspace name in the root `package.json`
7. **Changeset configuration** in `.changeset/config.json`:
   - Update `repo` field from `ascorbic/library-template` to your actual repository (e.g., `yourname/yourrepo`)
   - Review the `ignore` array and remove/update package names as needed for your project
8. **GitHub Secrets**: Set up required secrets in GitHub repository settings:
   - `APP_PRIVATE_KEY` - GitHub App private key for release workflow
   - `APP_ID` - GitHub App ID for release workflow
   - `CLAUDE_CODE_OAUTH_TOKEN` - Claude Code OAuth token for PR assistant
9. **npm Trusted Publishing**: Configure trusted publishing on npmjs.com for your packages to enable OIDC authentication (no NPM_TOKEN needed)

After setup, remove this section from CLAUDE.md.

## Repository Structure

This is a monorepo library template using pnpm workspaces with the following structure:

- **Root**: Workspace configuration and shared tooling
- **packages/**: Individual library packages (currently contains `example` package)
- **demos/**: Demo applications and examples

## Commands

### Root-level commands (run from repository root):

- `pnpm build` - Build all packages
- `pnpm test` - Run tests for all packages
- `pnpm check` - Run type checking and linting for all packages
- `pnpm format` - Format code using Prettier

### Package-level commands (run within individual packages):

- `pnpm build` - Build the package using tsdown (ESM + DTS output)
- `pnpm dev` - Watch mode for development
- `pnpm test` - Run vitest tests
- `pnpm check` - Run publint and @arethetypeswrong/cli checks

## Development Workflow

- Uses **pnpm** as package manager
- **tsdown** for building TypeScript packages with ESM output and declaration files
- **vitest** for testing
- **publint** and **@arethetypeswrong/cli** for package validation
- **Prettier** for code formatting (configured to use tabs in `.prettierrc`)

## Package Architecture

Each package in `packages/` follows this structure:

- `src/index.ts` - Main entry point
- `test/` - Test files
- `dist/` - Built output (ESM + .d.ts files)
- Package exports configured for ESM-only with proper TypeScript declarations

## TypeScript Configuration

Uses strict TypeScript configuration with:

- Target: ES2022
- Module: preserve (for bundler compatibility)
- Strict mode with additional safety checks (`noUncheckedIndexedAccess`, `noImplicitOverride`)
- Library-focused settings (declaration files, declaration maps)
