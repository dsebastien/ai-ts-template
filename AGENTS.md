# TODO

## Project overview

- Target: ...
- Entry point: ...

## Agent workflow and documentation

### Files to ignore

**NEVER read or modify
- `TODO.md`** at the project root.
- Files under `documentation/archived` unless instructed otherwise.

### Documentation

**IMPORTANT**:
- At the start of each new session, read the files in `documentation/` to understand the project, its current state and what should come next
- 

History is maintained in `documentation/history/yyyy-mm-dd.md` files, organized chronologically. Each file documents:
- What was accomplished that day
- Key decisions made
- Domain model changes
- Implementation progress
- Open questions or blockers

These files are optimized for conciseness and clarity to quickly onboard agents in new sessions.


### Business Rules Compliance

**CRITICAL**: Business rules documented in `documentation/Business Rules.md` MUST ALWAYS be respected unless explicit user approval is given to change or bypass them.

- **Mandatory compliance**: All implementations must respect documented business rules
- **No exceptions without approval**: Changing or bypassing any business rule requires explicit user approval
- **Highest priority**: When making changes, business rule compliance is of the utmost importance
- **Documentation requirement**: When a new business rule is mentioned, it must be immediately documented in `documentation/Business Rules.md` using a concise format (single line or paragraph) without losing precision

Read the Business Rules document at the start of each session to understand the constraints and requirements.

## Environment & tooling

- Node.js: use current LTS (Node 18+ recommended).
- **Package manager: npm** (required for this sample - `package.json` defines npm scripts and dependencies).

### Install

```bash
npm install
```

### Development Build (watch mode)

TODO

### Production Build

TODO

### Type Checking

This project uses **super strict TypeScript configuration**. Always ensure your code compiles without errors.

#### Quick Type Check

Use this to verify code compiles correctly without building:

```bash
npm run tsc
```

This runs `tsc --noEmit` which:
- Type checks all TypeScript files
- Reports compilation errors
- Does NOT generate output files
- Exits immediately with success/failure status

**When to use:**
- Before committing code
- To quickly verify changes compile
- **This is the recommended command for agents to verify compilation**

#### Continuous Type Checking (Optional)

For immediate feedback on type errors during development, you can optionally run type checking in watch mode:

```bash
npm run tsc:watch
```

This runs `tsc --noEmit --watch --preserveWatchOutput` which:
- Continuously watches for file changes
- Re-compiles automatically on save
- Shows compilation errors in real-time
- Preserves previous output for easier reading
- Does NOT generate output files

**When to use:** Keep this running in a separate terminal during active development for instant feedback on type errors

#### Before Committing

**ALWAYS** run before committing code:

```bash
npm run tsc
```

- Verifies all TypeScript code compiles without errors
- Does NOT generate output files (uses `--noEmit`)
- Must exit with zero errors before committing

## Linting

```bash
npx eslint main.ts ./src/**/*.ts
```

- Verifies all TypeScript code respects conventions
- Must exit with zero errors before committing


## File & folder conventions

- **Organize code into multiple files**: Split functionality across separate modules rather than putting everything in one file. Avoid very long files and prefer well-encapsulated and neatly-organized code
- Source lives in `src/`.

## Testing

TODO

## Versioning & releases

TODO

## Security, privacy, and compliance

TODO

## UX & copy guidelines

TODO

## Performance

- Keep startup light. Defer heavy work until needed.
- Use lazy initialization.
- Batch disk access
- Debounce/throttle expensive operations in response to system events.

## Coding conventions

### TypeScript Configuration

This project uses **super strict TypeScript configuration**. All code MUST respect the strict settings defined in `tsconfig.json`:

- ✅ `"strict": true` - All strict type checking options enabled
- ✅ `"noUnusedLocals": true` - No unused variables allowed
- ✅ `"noUnusedParameters": true` - No unused function parameters allowed
- ✅ `"noImplicitReturns": true` - All code paths must return a value
- ✅ `"noFallthroughCasesInSwitch": true` - No fallthrough in switch statements
- ✅ `"noUncheckedIndexedAccess": true` - Array/object access returns `T | undefined`
- ✅ `"noImplicitOverride": true` - Must use `override` keyword when overriding
- ✅ `"allowUnreachableCode": false` - No unreachable/dead code
- ✅ `"allowJs": false` - TypeScript only, no JavaScript files

**Always:**
- Check for null/undefined before accessing properties (use `if (!value) return` or optional chaining `value?.property`)
- Verify array/object access returns non-undefined before use (with `noUncheckedIndexedAccess`, `array[0]` returns `T | undefined`)
- Specify explicit return types for all functions
- Remove unused variables or prefix with `_` if intentionally unused
- Use `override` keyword when overriding parent class methods
- Ensure all switch statement cases are handled (no missing returns)
- Use `const` by default, `let` only when reassignment is needed, never `var`

**Common strict mode errors and fixes:**

```typescript
// 1. Missing override modifier (TS4114)
override async onload() { }  // ✓ Must use 'override' keyword

// 2. Uninitialized properties (TS2564)
settings!: PluginSettings;  // ✓ Use definite assignment if initialized in onload
settings: PluginSettings = DEFAULT_SETTINGS;  // ✓ Or initialize inline

// 3. Unchecked array access (noUncheckedIndexedAccess)
const first = array[0];
if (first) { /* use first */ }  // ✓ Must check, array[0] returns T | undefined

// 4. Missing return paths (TS7030)
function getValue(): string {
    if (condition) return 'yes';
    return 'no';  // ✓ All paths must return
}

// 5. Null checks (TS2531)
const file = this.app.workspace.getActiveFile();
if (!file) return;  // ✓ Check before use
```

### General Conventions

- **Keep the main entrypoint minimal**
- **Split large files**: If any file exceeds ~200-300 lines, consider breaking it into smaller, focused modules.
- **Use clear module boundaries**: Each file should have a single, well-defined responsibility.
- Bundle everything into the app (no unbundled runtime deps).
- Prefer `async/await` over promise chains; handle errors gracefully.

## Agent do/don't

**Do**
- Provide defaults and validation in settings.
- Write idempotent code paths and avoid leaking listeners or intervals.

**Don't**
- Introduce network calls without an obvious user-facing reason and documentation.
- Ship features that require cloud services without clear disclosure and explicit opt-in.

## Common tasks

TODO

## Troubleshooting

TODO
