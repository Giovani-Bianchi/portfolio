---
name: pr
description: Opens a Pull Request from the current branch to main with a standardized title and description derived from the commit and branch name.
metadata:
  author: Giovani Bianchi
  version: 1.0.0
---

Open a Pull Request from the current branch to `main` following the rules below.

## Deriving title and description

1. Read the current branch name with `git branch --show-current`
2. Read the latest commit with `git log -1 --pretty=format:"%s"` to use as the PR message base
3. If a scope is detectable from the commit or branch name (e.g. `feat/auth-login` → scope `auth`), include it. Otherwise omit it entirely.

## Breaking change detection

Before confirming the PR with the user, ask: **"Does this PR contain breaking changes? (y/n)"**

If yes, prepend `{BREAKING}` to the title.

## Title format

```
{BREAKING}[PREFIX](scope) #branch-name - commit message
```

- `{BREAKING}` — prepend **only** when user confirms breaking change; omit otherwise
- `PREFIX` in uppercase, wrapped in brackets
- `(scope)` in parentheses — **omit entirely if no scope is found**
- `#branch-name` using the exact current branch name
- Message: same as the squash commit message (no trailing period)

**Breaking with scope:** `{BREAKING}[FEAT](auth) #feat/auth-login - drop legacy auth api`
**With scope:** `[FEAT](auth) #feat/auth-login - add auth login page`
**Without scope:** `[CI] #ci/workflows - add deploy job to ci workflow`

## Prefix types

| Type       | Use                                                                |
| ---------- | ------------------------------------------------------------------ |
| `feat`     | New user-facing feature                                            |
| `fix`      | Bug fix                                                            |
| `refactor` | Change to existing feature that is neither a fix nor a new feature |
| `perf`     | Performance improvement                                            |
| `docs`     | Documentation addition or update                                   |
| `style`    | Code formatting changes (spacing, indentation, line breaks, etc.)  |
| `test`     | Test implementation or fix                                         |
| `build`    | Changes to the build process                                       |
| `ci`       | CI configuration or script changes                                 |
| `chore`    | General changes with no impact on application source code          |
| `deps`     | Dependency version updates                                         |
| `revert`   | Commit revert                                                      |

## Description format

List changes as concise bullet points:

```
- Added X
- Fixed Y
- Adjusted Z
```

Derive bullets from the diff (`git diff main...HEAD`) — do not invent items or collapse everything into one line.

## Execution steps

1. `git branch --show-current` — get branch name
2. `git log main...HEAD --pretty=format:"%s"` — list commits included in the PR
3. `git diff main...HEAD --stat` — get changed files for description context
4. Build title and description following the rules above
5. Confirm with the user before opening the PR
6. Open the PR with `gh pr create --base main --title "..." --body "..."`
