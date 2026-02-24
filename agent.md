# is-stream

## Overview

This is a Node.js library that provides utility functions to check if something is a Node.js stream. It supports checking for various stream types including Stream, Readable, Writable, Duplex, and Transform streams.

## Project Structure

- `index.js` - Main implementation file with all stream checking functions
- `index.d.ts` - TypeScript type definitions
- `test.js` - Ava test suite
- `index.test-d.ts` - TypeScript type tests using tsd
- `readme.md` - User-facing documentation
- `package.json` - Project configuration and dependencies

## Key Technologies

- **Runtime**: Node.js 18+
- **Module System**: ES modules (type: "module")
- **Testing Framework**: Ava for unit tests, tsd for TypeScript type tests
- **Linting**: XO (ESLint-based)
- **CI/CD**: GitHub Actions testing on Node.js 18 and 23

## Development Workflow

### Installing Dependencies

```bash
npm install
```

### Running Tests

```bash
npm test  # Runs xo (linting), ava (unit tests), and tsd (type tests)
```

### Running Individual Test Tools

```bash
npx xo          # Run linter only
npx ava         # Run unit tests only
npx tsd         # Run TypeScript type tests only
```

## API Functions

The library exports five main functions:

1. **isStream(stream, options?)** - Checks if something is a Stream
2. **isWritableStream(stream, options?)** - Checks if it's a Writable stream, OutgoingMessage, ServerResponse, or ClientRequest
3. **isReadableStream(stream, options?)** - Checks if it's a Readable stream or IncomingMessage
4. **isDuplexStream(stream, options?)** - Checks if it's a Duplex stream
5. **isTransformStream(stream, options?)** - Checks if it's a Transform stream

All functions accept an optional `options` parameter with a `checkOpen` boolean (default: true) that determines whether closed streams should return false.

## Code Style

- ES modules syntax (import/export)
- No semicolons at end of statements (handled by XO)
- Tab indentation
- Function implementation follows a pattern of checking properties and types
- All exports are named exports (no default export)

## Testing Guidelines

- Use Ava's test framework with descriptive test names
- Test both positive cases (should return true) and negative cases (should return false)
- Cover all stream types from Node.js: Stream, Readable, Writable, Duplex, Transform, PassThrough
- Test HTTP streams: OutgoingMessage, IncomingMessage, ServerResponse, ClientRequest
- Test network streams: net.Socket
- Test edge cases: {}, null, undefined, empty strings
- Use `temporaryFile()` from tempy for temporary file operations

## Important Implementation Details

- The library checks for specific properties to identify stream types
- `isStream()` checks for: pipe function, writable/readable properties
- `isWritableStream()` checks for: write, end functions, writable/writableObjectMode booleans, destroy function, destroyed boolean
- `isReadableStream()` checks for: read function, readable/readableObjectMode booleans, destroy function, destroyed boolean
- `isDuplexStream()` is a combination of isWritableStream and isReadableStream checks
- `isTransformStream()` additionally checks for the `_transform` function

## Making Changes

1. Modify the implementation in `index.js`
2. Update TypeScript types in `index.d.ts` if the API changes
3. Add/update tests in `test.js` for new functionality
4. Add/update type tests in `index.test-d.ts` for TypeScript changes
5. Update `readme.md` documentation if user-facing changes are made
6. Run `npm test` to ensure all tests pass and code is properly linted

## Common Tasks

### Adding a New Stream Check Function

1. Add the function implementation to `index.js`
2. Export the function from `index.js`
3. Add TypeScript type definitions to `index.d.ts`
4. Add comprehensive tests to `test.js`
5. Add TypeScript type tests to `index.test-d.ts`
6. Document the new function in `readme.md`

### Fixing a Bug

1. Write a failing test in `test.js` that demonstrates the bug
2. Fix the implementation in `index.js`
3. Verify the test now passes
4. Run full test suite to ensure no regressions

### Updating Dependencies

1. Update version in `package.json`
2. Run `npm install` to update lockfile
3. Run `npm test` to ensure compatibility
4. Check CI passes on both Node.js 18 and 23
