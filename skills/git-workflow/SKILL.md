---
name: git-workflow
description: Guides Git workflows, branching strategies, commit conventions, and collaboration patterns. Use when working with Git, creating PRs, managing branches, or when asked about version control.
---

# Git Workflow Skill

## Branching Strategies

### GitHub Flow (Recommended for most projects)
```
main ──●────●────●────●────●── (always deployable)
        \          /
feature  └──●──●──┘
```
- `main` is always deployable
- Feature branches from main
- PR + review + merge
- Deploy after merge

### Git Flow (For release-based projects)
```
main     ──●─────────────●────── (releases only)
            \           /
release      └────●────┘
                 /
develop  ──●──●────●──●──●──
            \     /
feature      └──●┘
```

## Commit Conventions

### Conventional Commits Format
```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

### Types
| Type | Description |
|------|-------------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Formatting, no logic change |
| `refactor` | Code change that neither fixes bug nor adds feature |
| `perf` | Performance improvement |
| `test` | Adding/updating tests |
| `chore` | Build process, dependencies |
| `ci` | CI configuration |

### Examples
```bash
feat(auth): add OAuth2 login support

Implements Google and GitHub OAuth providers.
Closes #123

BREAKING CHANGE: Session tokens now expire after 24h
```

```bash
fix(api): handle null response from payment gateway

Previously caused 500 error when gateway returned null.
Now returns appropriate error message to user.
```

## Branch Naming
```
<type>/<ticket-id>-<short-description>

# Examples
feature/AUTH-123-oauth-login
fix/BUG-456-null-pointer
chore/TECH-789-upgrade-deps
```

## PR Best Practices

### PR Template
```markdown
## Summary
[Brief description of changes]

## Changes
- [Change 1]
- [Change 2]

## Testing
- [ ] Unit tests added/updated
- [ ] Manual testing performed
- [ ] E2E tests pass

## Screenshots (if UI changes)
[Before/After screenshots]

## Checklist
- [ ] Code follows project conventions
- [ ] Documentation updated
- [ ] No security vulnerabilities introduced
```

### PR Size Guidelines
| Size | Lines Changed | Review Time |
|------|---------------|-------------|
| XS | < 50 | < 15 min |
| S | 50-200 | 15-30 min |
| M | 200-500 | 30-60 min |
| L | 500+ | Split if possible |

## Common Git Commands

### Daily Workflow
```bash
# Start new feature
git checkout main
git pull
git checkout -b feature/TICKET-123-description

# Commit changes
git add -p  # Stage interactively
git commit -m "feat: description"

# Keep up with main
git fetch origin main
git rebase origin/main

# Push and create PR
git push -u origin HEAD
```

### Fixing Mistakes
```bash
# Amend last commit (before push)
git commit --amend

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert a pushed commit
git revert <commit-hash>

# Interactive rebase to clean up
git rebase -i HEAD~3
```

### Advanced Operations
```bash
# Cherry-pick specific commit
git cherry-pick <commit-hash>

# Find which commit broke something
git bisect start
git bisect bad HEAD
git bisect good <known-good-commit>

# Stash with message
git stash push -m "WIP: feature description"
git stash list
git stash pop
```
