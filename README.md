# Haskell Plugin for Codex

Haskell development skills and hooks for Codex.

## Installation

Install this repository as a local Codex plugin, or publish it through a Codex marketplace entry that points at this plugin directory.

```bash
git clone git@github.com:birdgg/haskell-plugin.git
```

## Components

### Skills

| Skill | Description |
|-------|-------------|
| `haskell-build` | Build with `cabal`/`stack`, parse GHC errors, and apply safe fixes |
| `haskell-test` | Run HSpec/QuickCheck/Tasty tests and report results |
| `haskell-reviewer` | Code review for idiomatic Haskell, type safety, purity, and performance |
| `haskell-patterns` | Idiomatic Haskell conventions: newtypes, smart constructors, ReaderT, error handling, concurrency |
| `haskell-effectful` | Effectful library conventions: dispatch choice, effect stack order, custom effects, concurrency |
| `haskell-relude` | Relude conventions: Text-first, safe alternatives, container types, lifted IO |
| `haskell-servant` | Servant web framework conventions: NamedRoutes record pattern, CRUD APIs, auth, testing |
| `haskell-servant-client` | Servant client API wrapper conventions: two-layer error handling, NFData/Exception, effectful integration |

### Hooks

| Hook | Trigger | Description |
|------|---------|-------------|
| HLint | PostToolUse (Edit/Write) | Runs HLint on `.hs` files after editing |

## Codex Manifest

Codex reads plugin metadata from `.codex-plugin/plugin.json`. This plugin exposes the `skills/` directory and `hooks/hooks.json` through that manifest.

The original Claude plugin files are still present for reference/backward compatibility:

- `.claude-plugin/plugin.json`
- `.claude-plugin/marketplace.json`
- `commands/`
- `agents/`

## Prerequisites

- GHC and `cabal-install` or `stack`
- `hlint` (optional): `cabal install hlint`

## Structure

```
haskell-plugin/
├── .codex-plugin/
│   └── plugin.json
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── commands/
│   ├── haskell-build.md
│   └── haskell-test.md
├── agents/
│   └── haskell-reviewer.md
├── skills/
│   ├── haskell-build/
│   │   └── SKILL.md
│   ├── haskell-test/
│   │   └── SKILL.md
│   ├── haskell-reviewer/
│   │   └── SKILL.md
│   ├── haskell-patterns/
│   │   └── SKILL.md
│   ├── haskell-effectful/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── effectful-examples.md
│   ├── haskell-relude/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── relude-migration.md
│   ├── haskell-servant/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── servant-examples.md
│   └── haskell-servant-client/
│       ├── SKILL.md
│       └── references/
│           └── servant-client-examples.md
├── hooks/
│   └── hooks.json
└── README.md
```
