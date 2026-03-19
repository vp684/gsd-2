# Local Development Guide

This guide explains how to modify and run a local version of GSD 2 from its source code.

## Prerequisites

- **Node.js** ≥ 22.0.0 (24 LTS recommended)
- **npm** 10.9.3 or compatible
- **Git**

## Quick Start

### 1. Clone and Install

```bash
git clone https://github.com/gsd-build/gsd-2.git
cd gsd-2
npm install
```

### 2. Build the Project

```bash
npm run build
```

This compiles TypeScript and copies resources. The entry point is `dist/loader.js`.

### 3. Link Locally

```bash
npm link
```

This creates a global symlink so `gsd` in any terminal uses your local development version.

### 4. Test Your Changes

```bash
# Run the CLI from your local build
node dist/loader.js

# Or use the symlinked gsd command
gsd
```

## Development Workflow

### Hot Reload Development

For faster iteration during development:

```bash
npm run dev
```

### Running Tests

```bash
# Unit tests only
npm run test:unit

# Integration tests
npm run test:integration

# All tests
npm run test

# Smoke tests
npm run test:smoke
```

### Clean Rebuild

If you need a fresh build:

```bash
rm -rf dist/
npm run build
```

## Project Structure

```
gsd-2/
├── dist/                    # Compiled output (generated)
├── src/                     # Source code
│   └── resources/
│       ├── extensions/      # Bundled extensions
│       └── agents/          # Bundled subagents
├── packages/                # Workspace packages
│   ├── pi-tui/             # Terminal UI
│   ├── pi-ai/              # AI abstractions
│   ├── pi-agent-core/      # Agent core
│   └── pi-coding-agent/    # Coding agent
├── scripts/                 # Build scripts
├── native/                  # Native bindings
└── docs/                    # Documentation
```

## Key Build Commands

| Command | Description |
|---------|-------------|
| `npm run build` | Full build (PI SDK + TypeScript + resources) |
| `npm run build:pi` | Build PI SDK packages only |
| `npm run build:native` | Build native bindings |
| `npm run dev` | Development mode with hot reload |

## Unlink (When Done)

```bash
npm unlink
npm install -g gsd-pi  # reinstall official version
```

## Troubleshooting

### Build Errors

If you encounter build errors, try:

```bash
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Native Module Errors

Native modules require platform-specific builds. If you see errors about native bindings:

```bash
npm run build:native
```

### TypeScript Errors

Run type checking:

```bash
npm run typecheck:extensions
```

## Next Steps

- Read the [Architecture Overview](./architecture.md) to understand how GSD works
- Check the [Configuration Guide](./configuration.md) for customizing GSD
- Explore [Extending Pi](./extending-pi/README.md) to add custom functionality
