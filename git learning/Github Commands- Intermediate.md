# Introduction to GitHub — Intermediate

---

## 1. Branching Strategies

A branching strategy defines how your team uses branches to organize work. Picking the right one keeps your codebase clean and your team sane.

### 1.1 Git Flow

The classic strategy for projects with scheduled releases.

```
main          ──●────────────────────────────●── (production)
                │                            │
hotfix        ──┼──────────●────────────────┤
                │           │               │
release/1.0   ──┼───────────┼──●────────────┤
                │           │  │            │
develop       ──●──●──●──●──●──●──●──●──●──●──
                   │     │
feature/login ─────●──●──┘
feature/dash  ───────────●──●──┘
```

| Branch | Purpose |
|--------|---------|
| `main` | Production-ready code only |
| `develop` | Integration branch for features |
| `feature/*` | Individual features, branch off develop |
| `release/*` | Pre-release stabilization |
| `hotfix/*` | Emergency production fixes |

### 1.2 GitHub Flow

Simpler — ideal for continuous deployment teams.

```
main  ──●──────────────────────●── (always deployable)
         └──●──●──●──PR──merge─┘
            feature/my-feature
```

| Step | Action |
|------|--------|
| 1 | Branch off `main` |
| 2 | Commit your changes |
| 3 | Open a Pull Request |
| 4 | Review & discuss |
| 5 | Deploy and test |
| 6 | Merge to `main` |

### 1.3 Trunk Based Development

Everyone commits to `main` (trunk) frequently — feature flags hide incomplete work.

| Strategy | Best For | Release Cadence |
|----------|----------|-----------------|
| Git Flow | Large teams, versioned releases | Scheduled (weekly/monthly) |
| GitHub Flow | Small teams, web apps | Continuous |
| Trunk Based | High-performing teams, CI/CD | Multiple times per day |

---

## 2. Advanced Branching Commands

| Command | Description | Example |
|--------|-------------|---------|
| `git branch -a` | List all local + remote branches | `git branch -a` |
| `git branch -r` | List only remote branches | `git branch -r` |
| `git branch --merged` | Branches already merged into current | `git branch --merged` |
| `git branch --no-merged` | Branches not yet merged | `git branch --no-merged` |
| `git push origin --delete <branch>` | Delete remote branch | `git push origin --delete feature/login` |
| `git fetch --prune` | Remove local refs to deleted remote branches | `git fetch --prune` |
| `git switch -c <branch> origin/<branch>` | Track a remote branch locally | `git switch -c feature/x origin/feature/x` |

---

## 3. Merging vs Rebasing

This is one of the most important concepts at the intermediate level.

### 3.1 Merge

Combines two branches by creating a **merge commit** — preserves full history.

```
Before:
main      ──●──●──●
                   \
feature         ●──●

After git merge:
main      ──●──●──●──────M──  (M = merge commit)
                   \    /
feature         ●──●──┘
```

### 3.2 Rebase

Moves your branch commits on top of another branch — creates **linear history**.

```
Before:
main      ──●──●──●
                   \
feature         ●──●

After git rebase main:
main      ──●──●──●──●'──●'──  (replayed commits)
```

### 3.3 Merge vs Rebase Comparison

| | Merge | Rebase |
|--|-------|--------|
| History | Preserves full history | Creates clean linear history |
| Merge commit | ✅ Creates one | ❌ No merge commit |
| Safe on shared branches | ✅ Yes | ⚠️ Never rebase shared branches |
| Traceability | Full context | Cleaner log |
| When to use | Team branches, main | Local cleanup before PR |

### 3.4 Rebase Commands

| Command | Description | Example |
|--------|-------------|---------|
| `git rebase <branch>` | Rebase current branch onto another | `git rebase main` |
| `git rebase -i HEAD~3` | Interactive rebase of last 3 commits | `git rebase -i HEAD~3` |
| `git rebase --continue` | Continue after resolving conflicts | `git rebase --continue` |
| `git rebase --abort` | Cancel rebase | `git rebase --abort` |
| `git rebase --skip` | Skip current conflicting commit | `git rebase --skip` |

---

## 4. Interactive Rebase — Rewriting History

Interactive rebase (`git rebase -i`) lets you clean up commits before sharing.

### 4.1 Interactive Rebase Commands

| Command | What It Does |
|---------|-------------|
| `pick` | Keep commit as-is |
| `reword` | Keep commit but edit message |
| `edit` | Pause to amend the commit |
| `squash` | Combine with previous commit (keep both messages) |
| `fixup` | Combine with previous commit (discard this message) |
| `drop` | Delete this commit entirely |
| `reorder` | Move lines to reorder commits |

### 4.2 Example — Squashing 3 commits into 1

```bash
git rebase -i HEAD~3

# Editor opens:
pick a1b2c3 add login form
pick d4e5f6 fix typo in login
pick g7h8i9 fix another typo

# Change to:
pick a1b2c3 add login form
fixup d4e5f6 fix typo in login
fixup g7h8i9 fix another typo

# Result: single clean commit "add login form"
```

---

## 5. Conflict Resolution

Conflicts happen when two branches change the same part of the same file.

### 5.1 What a Conflict Looks Like

```
<<<<<<< HEAD (your branch)
const port = 3000;
=======
const port = 8080;
>>>>>>> feature/config
```

### 5.2 Resolving Conflicts Step by Step

```bash
# Step 1 — Git tells you there's a conflict
git merge feature/config
# CONFLICT (content): Merge conflict in config.js

# Step 2 — Open the file and resolve manually
# Edit the file to keep what you want, remove the markers

# Step 3 — Mark as resolved
git add config.js

# Step 4 — Complete the merge
git commit
```

### 5.3 Conflict Resolution Tools

| Command | Description |
|--------|-------------|
| `git status` | Shows which files have conflicts |
| `git diff` | Shows conflict markers in detail |
| `git mergetool` | Open visual merge tool |
| `git checkout --ours <file>` | Keep your version entirely |
| `git checkout --theirs <file>` | Keep their version entirely |
| `git log --merge` | Show commits causing the conflict |

---

## 6. Stashing

Stash lets you save uncommitted work temporarily and come back to it later.

```
Working Directory  →  git stash  →  Stash Stack
     (clean)                        (saved work)
         ↑                               │
         └──────── git stash pop ────────┘
```

| Command | Description | Example |
|--------|-------------|---------|
| `git stash` | Stash current changes | `git stash` |
| `git stash push -m "message"` | Stash with a description | `git stash push -m "wip login"` |
| `git stash list` | View all stashes | `git stash list` |
| `git stash pop` | Apply latest stash and remove it | `git stash pop` |
| `git stash apply stash@{2}` | Apply specific stash, keep it | `git stash apply stash@{2}` |
| `git stash drop stash@{0}` | Delete a specific stash | `git stash drop stash@{0}` |
| `git stash clear` | Delete all stashes | `git stash clear` |
| `git stash branch <name>` | Create branch from stash | `git stash branch feature/wip` |
| `git stash -u` | Stash including untracked files | `git stash -u` |

---

## 7. Tags & Releases

Tags mark specific points in history — typically used for version releases.

### 7.1 Tag Types

| Type | Description |
|------|-------------|
| **Lightweight** | Just a pointer to a commit — no extra info |
| **Annotated** | Full object with tagger name, date, message — recommended |

### 7.2 Tag Commands

| Command | Description | Example |
|--------|-------------|---------|
| `git tag` | List all tags | `git tag` |
| `git tag <name>` | Create lightweight tag | `git tag v1.0` |
| `git tag -a <name> -m "msg"` | Create annotated tag | `git tag -a v1.0 -m "First release"` |
| `git tag -a <name> <commit>` | Tag a past commit | `git tag -a v0.9 a1b2c3` |
| `git show <tag>` | Show tag details | `git show v1.0` |
| `git push origin <tag>` | Push specific tag to GitHub | `git push origin v1.0` |
| `git push origin --tags` | Push all tags | `git push origin --tags` |
| `git tag -d <name>` | Delete local tag | `git tag -d v1.0` |
| `git push origin --delete <tag>` | Delete remote tag | `git push origin --delete v1.0` |
| `git checkout <tag>` | Check out code at a tag | `git checkout v1.0` |

---

## 8. Pull Requests — In Depth

### 8.1 PR Best Practices

| Practice | Why It Matters |
|----------|---------------|
| Keep PRs small and focused | Easier to review, faster to merge |
| Write a clear PR description | Reviewers need context |
| Link related issues | Ties code to requirements (`Closes #42`) |
| Add screenshots for UI changes | Visual confirmation for reviewers |
| Respond to all review comments | Shows respect for reviewer's time |
| Don't force-push after review starts | Invalidates existing review comments |
| Request specific reviewers | Gets the right eyes on the right code |

### 8.2 PR Description Template

```markdown
## What does this PR do?
Brief description of the change.

## Why?
Context — what problem does this solve?

## How to test
1. Step one
2. Step two
3. Expected result

## Screenshots (if applicable)

## Related Issues
Closes #42
```

### 8.3 Review States

| State | Meaning |
|-------|---------|
| **Comment** | General feedback, no approval/rejection |
| **Approve** | LGTM — ready to merge |
| **Request Changes** | Must fix before merging |

### 8.4 Merging Options on GitHub

| Option | What It Does | When to Use |
|--------|-------------|-------------|
| **Merge commit** | Keeps all commits + adds merge commit | Full history needed |
| **Squash and merge** | Squashes all PR commits into one | Clean main branch history |
| **Rebase and merge** | Replays commits on top of main | Linear history without merge commit |

---

## 9. GitHub Issues

Issues are how work gets tracked — bugs, features, tasks, questions.

### 9.1 Issue Best Practices

| Element | Description |
|---------|-------------|
| **Title** | Clear and specific — what exactly is the problem |
| **Description** | Steps to reproduce, expected vs actual behavior |
| **Labels** | Categorize: `bug`, `enhancement`, `documentation`, `help wanted` |
| **Assignees** | Who is responsible |
| **Milestone** | Which release this belongs to |
| **Linked PR** | The PR that fixes this issue |

### 9.2 Closing Issues via Commits

Add these keywords in a commit message or PR description to auto-close an issue on merge:

| Keyword | Example |
|---------|---------|
| `Closes #n` | `Closes #42` |
| `Fixes #n` | `Fixes #42` |
| `Resolves #n` | `Resolves #42` |

---

## 10. GitHub Actions — CI/CD Basics

GitHub Actions automates your workflow — run tests, lint code, and deploy on every push or PR.

### 10.1 Key Concepts

| Concept | Description |
|---------|-------------|
| **Workflow** | Automated process defined in a `.yml` file |
| **Event** | What triggers the workflow (push, PR, schedule) |
| **Job** | A set of steps that run on the same runner |
| **Step** | Individual task inside a job |
| **Runner** | The virtual machine that runs the job |
| **Action** | Reusable step from GitHub Marketplace |

### 10.2 Workflow File Location

```
your-repo/
└── .github/
    └── workflows/
        ├── ci.yml
        └── deploy.yml
```

### 10.3 Example — Run Tests on Every Push

```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

### 10.4 Common Workflow Triggers

| Trigger | Description |
|---------|-------------|
| `push` | On any push to specified branches |
| `pull_request` | On PR open, update, or sync |
| `schedule` | Cron-based (e.g. nightly builds) |
| `workflow_dispatch` | Manual trigger from GitHub UI |
| `release` | When a release is published |

---

## 11. GitHub Secrets & Environment Variables

Never hardcode API keys or passwords in your code. Store them as GitHub Secrets.

### 11.1 Setting Secrets

```
GitHub Repo → Settings → Secrets and variables → Actions → New repository secret
```

### 11.2 Using Secrets in Workflows

```yaml
steps:
  - name: Deploy to server
    env:
      API_KEY: ${{ secrets.API_KEY }}
      DB_PASSWORD: ${{ secrets.DB_PASSWORD }}
    run: ./deploy.sh
```

### 11.3 Secret Scopes

| Scope | Description |
|-------|-------------|
| **Repository secrets** | Available to one repo only |
| **Environment secrets** | Tied to a deployment environment (staging, prod) |
| **Organization secrets** | Shared across multiple repos in an org |

---

## 12. Git Hooks

Git hooks are scripts that run automatically at specific points in the Git workflow.

### 12.1 Hook Types

| Hook | Trigger | Common Use |
|------|---------|------------|
| `pre-commit` | Before a commit is created | Run linter, formatter |
| `commit-msg` | After commit message is entered | Enforce message format |
| `pre-push` | Before pushing to remote | Run tests |
| `post-merge` | After a merge completes | Install dependencies |
| `pre-rebase` | Before rebasing | Safety check |

### 12.2 Creating a Hook

```bash
# Hooks live in .git/hooks/
nano .git/hooks/pre-commit

#!/bin/bash
npm run lint
if [ $? -ne 0 ]; then
  echo "Linting failed. Commit aborted."
  exit 1
fi

# Make it executable
chmod +x .git/hooks/pre-commit
```

### 12.3 Husky — Team-Wide Hooks

```bash
# Install husky (Node.js projects)
npm install --save-dev husky
npx husky init

# Add a pre-commit hook
echo "npm run lint" > .husky/pre-commit
```

---

## 13. Forking & Contributing to Open Source

### 13.1 Full Open Source Contribution Workflow

```bash
# 1. Fork on GitHub (click Fork button)

# 2. Clone your fork
git clone https://github.com/you/project.git
cd project

# 3. Add the original repo as upstream
git remote add upstream https://github.com/original/project.git

# 4. Verify remotes
git remote -v
# origin    https://github.com/you/project.git (your fork)
# upstream  https://github.com/original/project.git (original)

# 5. Create a feature branch
git switch -c feat/my-contribution

# 6. Make changes, commit
git add .
git commit -m "feat: add contribution"

# 7. Keep your fork updated before pushing
git fetch upstream
git rebase upstream/main

# 8. Push to your fork
git push origin feat/my-contribution

# 9. Open a Pull Request on GitHub
```

### 13.2 Keeping Your Fork in Sync

| Command | Description |
|--------|-------------|
| `git fetch upstream` | Get latest from original repo |
| `git rebase upstream/main` | Replay your commits on top of latest main |
| `git merge upstream/main` | Merge upstream changes into your branch |
| `git push origin main --force-with-lease` | Update your fork's main safely |

---

## 14. Advanced Log & Search

| Command | Description | Example |
|--------|-------------|---------|
| `git log --oneline --graph --all` | Visual graph of all branches | `git log --oneline --graph --all` |
| `git log --author="John"` | Commits by specific author | `git log --author="John"` |
| `git log --since="2 weeks ago"` | Commits in last 2 weeks | `git log --since="2 weeks ago"` |
| `git log --grep="fix"` | Commits with "fix" in message | `git log --grep="fix"` |
| `git log -S "functionName"` | Commits that added/removed a string | `git log -S "getUserById"` |
| `git log -- <file>` | History of a specific file | `git log -- src/auth.js` |
| `git shortlog -sn` | Commit count per author | `git shortlog -sn` |
| `git bisect start` | Start binary search for a bug | `git bisect start` |
| `git bisect bad` | Mark current commit as bad | `git bisect bad` |
| `git bisect good <commit>` | Mark a known good commit | `git bisect good a1b2c3` |
| `git bisect reset` | End bisect session | `git bisect reset` |

---

## 15. cherry-pick

Cherry-pick applies a specific commit from one branch onto another — without merging the whole branch.

```
main     ──●──●──●──────────●'──
              │              ↑
feature  ──●──●──●──●       cherry-picked
                  ↑
              this commit only
```

| Command | Description | Example |
|--------|-------------|---------|
| `git cherry-pick <commit>` | Apply a single commit | `git cherry-pick a1b2c3` |
| `git cherry-pick <c1>..<c2>` | Apply a range of commits | `git cherry-pick a1b..d4e` |
| `git cherry-pick --no-commit <c>` | Apply changes without committing | `git cherry-pick --no-commit a1b2c3` |
| `git cherry-pick --abort` | Cancel cherry-pick | `git cherry-pick --abort` |
| `git cherry-pick --continue` | Continue after conflict resolution | `git cherry-pick --continue` |

---

## 16. Key Things to Always Remember

| Rule | Why It Matters |
|------|----------------|
| Never rebase shared/public branches | Rewrites history — breaks everyone else's repo |
| Squash before merging to main | Keeps main history clean and readable |
| Always fetch before rebase | Ensures you're rebasing on the latest |
| Use `--force-with-lease` not `--force` | Safer force push — won't overwrite others' work |
| Keep PRs focused and small | Faster reviews, fewer conflicts |
| Tag every release | Makes rollbacks and changelogs straightforward |
| Protect the main branch | Require PRs + reviews before merging |
| Use branch protection rules on GitHub | Prevents accidental direct pushes to main |

---
