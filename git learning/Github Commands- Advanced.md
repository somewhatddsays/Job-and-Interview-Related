# Introduction to GitHub — Advanced

---

## 1. Git Internals — How Git Actually Works

Understanding Git's internals makes you dangerous in the best way possible.

### 1.1 The Object Model

Everything in Git is stored as one of four object types in `.git/objects/`.

| Object | Description | Created By |
|--------|-------------|------------|
| **blob** | Raw file content | `git add` |
| **tree** | Directory listing (points to blobs + trees) | `git commit` |
| **commit** | Snapshot — points to a tree + parent commit | `git commit` |
| **tag** | Annotated tag object | `git tag -a` |

```
commit a1b2c3
│
├── tree f4e5d6  (root directory)
│   ├── blob 1a2b3c  (README.md content)
│   ├── blob 4d5e6f  (main.js content)
│   └── tree 7g8h9i  (src/ directory)
│       └── blob 0j1k2l  (src/app.js content)
│
└── parent 9z8y7x  (previous commit)
```

### 1.2 Inspecting Git Objects

| Command | Description | Example |
|--------|-------------|---------|
| `git cat-file -t <hash>` | Show object type | `git cat-file -t a1b2c3` |
| `git cat-file -p <hash>` | Pretty-print object contents | `git cat-file -p a1b2c3` |
| `git ls-tree <tree-hash>` | List contents of a tree object | `git ls-tree HEAD` |
| `git ls-tree -r HEAD` | Recursively list all files | `git ls-tree -r HEAD` |
| `git rev-parse HEAD` | Get full SHA of HEAD | `git rev-parse HEAD` |
| `git rev-parse HEAD~3` | SHA of 3 commits before HEAD | `git rev-parse HEAD~3` |
| `git hash-object <file>` | Get SHA of a file without adding | `git hash-object file.txt` |
| `git count-objects -v` | Count loose objects in repo | `git count-objects -v` |

### 1.3 The .git Directory

```
.git/
├── HEAD              → Points to current branch (ref: refs/heads/main)
├── config            → Repo-level Git config
├── index             → Staging area (binary file)
├── COMMIT_EDITMSG    → Last commit message
├── objects/          → All Git objects (blobs, trees, commits, tags)
│   ├── pack/         → Packed objects for efficiency
│   └── info/
├── refs/
│   ├── heads/        → Local branch pointers
│   ├── remotes/      → Remote tracking branches
│   └── tags/         → Tag pointers
├── logs/
│   ├── HEAD          → History of HEAD movements
│   └── refs/heads/   → History of each branch
└── hooks/            → Git hook scripts
```

### 1.4 Refs & Reflog

| Command | Description | Example |
|--------|-------------|---------|
| `git reflog` | History of every HEAD movement | `git reflog` |
| `git reflog show <branch>` | Reflog for a specific branch | `git reflog show main` |
| `git reflog expire --all` | Expire old reflog entries | — |
| `cat .git/HEAD` | See what HEAD points to | `cat .git/HEAD` |
| `git show HEAD@{3}` | Show state 3 moves ago | `git show HEAD@{3}` |
| `git checkout HEAD@{5}` | Restore to 5 moves ago | `git checkout HEAD@{5}` |

> **Golden Rule:** As long as an object exists in reflog, it can be recovered — even after `reset --hard`.

---

## 2. Advanced Rebase Techniques

### 2.1 Rebase onto a Specific Commit

```bash
# Move feature branch to start from a different point
git rebase --onto <newbase> <oldbase> <branch>

# Example: Move feature/x off develop onto main
git rebase --onto main develop feature/x
```

### 2.2 Exec in Interactive Rebase

Run a shell command after each commit during rebase:

```bash
git rebase -i HEAD~5

# In editor:
pick a1b2c3 add feature
exec npm test          ← runs tests after this commit
pick d4e5f6 fix bug
exec npm test
pick g7h8i9 refactor
```

### 2.3 Autosquash

Automatically squash commits marked with `fixup!` or `squash!`:

```bash
# Create a fixup commit targeting an earlier one
git commit --fixup a1b2c3

# Then autosquash during rebase
git rebase -i --autosquash HEAD~5
```

### 2.4 Rebase Strategies Comparison

| Scenario | Command |
|----------|---------|
| Clean up local commits before PR | `git rebase -i HEAD~n` |
| Update branch with latest main | `git rebase main` |
| Move branch to different base | `git rebase --onto newbase oldbase branch` |
| Replay single branch on remote | `git pull --rebase origin main` |

---

## 3. Advanced Reset, Revert & Restore

### 3.1 Reset Reference Chart

```
HEAD~1 ──────── HEAD ──────── Index ──────── Working Dir
  (last)       (current)    (staging)         (files)

git reset --soft  HEAD~1   → moves HEAD only, staging + files untouched
git reset --mixed HEAD~1   → moves HEAD + clears staging, files untouched
git reset --hard  HEAD~1   → moves HEAD + clears staging + discards file changes
```

### 3.2 Advanced Reset Commands

| Command | Description | Example |
|--------|-------------|---------|
| `git reset HEAD~n` | Undo last n commits (mixed) | `git reset HEAD~3` |
| `git reset <commit> -- <file>` | Reset single file to a commit | `git reset a1b2c3 -- src/app.js` |
| `git reset --hard origin/main` | Reset local to match remote exactly | `git reset --hard origin/main` |
| `git revert HEAD~3..HEAD` | Revert a range of commits | `git revert HEAD~3..HEAD` |
| `git revert -n HEAD~3..HEAD` | Revert range without committing | `git revert -n HEAD~3..HEAD` |
| `git restore --source=<commit> <file>` | Restore file from specific commit | `git restore --source=a1b2c3 app.js` |

### 3.3 Recovering Lost Commits

```bash
# Step 1 — Find the lost commit in reflog
git reflog

# Step 2 — Identify the SHA
# e.g. a1b2c3 HEAD@{4}: commit: my lost commit

# Step 3 — Recover it
git checkout -b recovery/branch a1b2c3
# OR cherry-pick it back
git cherry-pick a1b2c3
```

---

## 4. Advanced GitHub Actions

### 4.1 Matrix Builds

Test across multiple OS / versions simultaneously:

```yaml
jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        node: [18, 20, 22]
      fail-fast: false   # don't cancel others if one fails

    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
      - run: npm ci
      - run: npm test
```

### 4.2 Reusable Workflows

Define once, call from many workflows:

```yaml
# .github/workflows/reusable-test.yml
on:
  workflow_call:
    inputs:
      environment:
        required: true
        type: string
    secrets:
      API_KEY:
        required: true

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Testing ${{ inputs.environment }}"
```

```yaml
# .github/workflows/ci.yml — calling the reusable workflow
jobs:
  call-test:
    uses: ./.github/workflows/reusable-test.yml
    with:
      environment: staging
    secrets:
      API_KEY: ${{ secrets.API_KEY }}
```

### 4.3 Concurrency Control

Prevent multiple deployments running at the same time:

```yaml
concurrency:
  group: deploy-${{ github.ref }}
  cancel-in-progress: true   # cancel previous run if new one starts
```

### 4.4 Caching Dependencies

```yaml
- name: Cache node_modules
  uses: actions/cache@v4
  with:
    path: ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-node-
```

### 4.5 Deployment Environments

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: production
      url: https://myapp.com   # shown in GitHub UI
    steps:
      - run: ./deploy.sh
```

### 4.6 Job Dependencies & Outputs

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.get-version.outputs.version }}
    steps:
      - id: get-version
        run: echo "version=$(cat VERSION)" >> $GITHUB_OUTPUT

  deploy:
    needs: build    # runs only after build succeeds
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying version ${{ needs.build.outputs.version }}"
```

### 4.7 Self-Hosted Runners

| Command | Description |
|--------|-------------|
| Register runner via GitHub UI | Settings → Actions → Runners → New self-hosted runner |
| `./run.sh` | Start the runner agent |
| `runs-on: self-hosted` | Use self-hosted runner in workflow |
| Labels | Target specific runners with custom labels |

---

## 5. GitHub Security Features

### 5.1 Branch Protection Rules

```
Repo → Settings → Branches → Add rule
```

| Rule | Description |
|------|-------------|
| Require PR before merging | No direct pushes to protected branch |
| Require approvals | Minimum number of review approvals |
| Dismiss stale reviews | Re-review required after new pushes |
| Require status checks | CI must pass before merge |
| Require linear history | No merge commits — squash or rebase only |
| Require signed commits | Commits must be GPG signed |
| Include administrators | Rules apply to admins too |
| Allow force pushes | Enable/disable for specific users |

### 5.2 Commit Signing with GPG

```bash
# Generate GPG key
gpg --full-generate-key

# List keys and get key ID
gpg --list-secret-keys --keyid-format=long

# Export public key and add to GitHub
gpg --armor --export <KEY_ID>
# GitHub → Settings → SSH and GPG keys → New GPG key

# Tell Git to sign commits
git config --global user.signingkey <KEY_ID>
git config --global commit.gpgsign true

# Sign a specific commit manually
git commit -S -m "signed commit"

# Verify a commit signature
git log --show-signature
git verify-commit <hash>
```

### 5.3 Dependabot

Automated dependency updates and security alerts.

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10
    reviewers:
      - "your-username"
    labels:
      - "dependencies"

  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "monthly"
```

### 5.4 Code Scanning with CodeQL

```yaml
# .github/workflows/codeql.yml
name: CodeQL

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 2 * * 1'  # every Monday at 2am

jobs:
  analyze:
    runs-on: ubuntu-latest
    permissions:
      security-events: write

    steps:
      - uses: actions/checkout@v4
      - uses: github/codeql-action/init@v3
        with:
          languages: javascript, python
      - uses: github/codeql-action/autobuild@v3
      - uses: github/codeql-action/analyze@v3
```

### 5.5 Secret Scanning & Push Protection

| Feature | Description |
|---------|-------------|
| **Secret scanning** | Automatically detects secrets pushed to repos |
| **Push protection** | Blocks pushes containing detected secrets |
| **Custom patterns** | Define regex patterns for proprietary secrets |
| **Bypass** | Allowed with justification for false positives |

---

## 6. Git Worktrees

Work on multiple branches simultaneously in separate directories — no stashing required.

```bash
# Add a worktree for a branch
git worktree add ../hotfix-branch hotfix/critical-bug

# Now you have:
# /project           → main branch
# /hotfix-branch     → hotfix/critical-bug branch

# List all worktrees
git worktree list

# Remove a worktree
git worktree remove ../hotfix-branch

# Prune stale worktree metadata
git worktree prune
```

---

## 7. Submodules & Subtrees

### 7.1 Git Submodules

Include one repo inside another — the inner repo stays independent.

| Command | Description | Example |
|--------|-------------|---------|
| `git submodule add <url> <path>` | Add a submodule | `git submodule add https://github.com/user/lib.git libs/mylib` |
| `git submodule init` | Initialize submodules after cloning | `git submodule init` |
| `git submodule update` | Pull submodule contents | `git submodule update` |
| `git submodule update --init --recursive` | Init + update all nested submodules | — |
| `git submodule foreach git pull` | Update all submodules | — |
| `git submodule status` | Show submodule SHAs | `git submodule status` |
| `git rm <submodule-path>` | Remove a submodule | `git rm libs/mylib` |
| `git clone --recurse-submodules <url>` | Clone with all submodules | — |

### 7.2 Git Subtrees

Merge another repo into a subdirectory — simpler than submodules for contributors.

```bash
# Add a subtree
git subtree add --prefix=libs/mylib https://github.com/user/lib.git main --squash

# Pull latest from subtree remote
git subtree pull --prefix=libs/mylib https://github.com/user/lib.git main --squash

# Push changes back to subtree remote
git subtree push --prefix=libs/mylib https://github.com/user/lib.git main
```

### 7.3 Submodules vs Subtrees

| | Submodules | Subtrees |
|--|-----------|----------|
| Repo independence | Separate repo pointer | Code copied in |
| Contributor complexity | Higher — must init/update | Lower — works out of the box |
| Pushing upstream | Hard | Easier with `subtree push` |
| History | Separate | Merged into main repo |
| Best for | Shared libraries, SDKs | Internal shared code |

---

## 8. Advanced GitHub CLI (gh)

The `gh` CLI lets you do everything GitHub does — from the terminal.

### 8.1 Installation & Auth

```bash
# Install (Ubuntu)
sudo apt install gh

# Authenticate
gh auth login

# Check status
gh auth status
```

### 8.2 Repos

| Command | Description |
|--------|-------------|
| `gh repo create` | Create a new repo interactively |
| `gh repo create <n> --public` | Create public repo |
| `gh repo clone <user/repo>` | Clone a repo |
| `gh repo fork <user/repo>` | Fork a repo |
| `gh repo view` | View repo info in terminal |
| `gh repo view --web` | Open repo in browser |
| `gh repo list` | List your repos |

### 8.3 Pull Requests

| Command | Description |
|--------|-------------|
| `gh pr create` | Create a PR interactively |
| `gh pr create --title "fix" --body "desc"` | Create PR with title and body |
| `gh pr list` | List open PRs |
| `gh pr view <n>` | View a specific PR |
| `gh pr checkout <n>` | Checkout a PR branch locally |
| `gh pr review <n> --approve` | Approve a PR |
| `gh pr review <n> --request-changes -b "reason"` | Request changes |
| `gh pr merge <n> --squash` | Merge PR with squash |
| `gh pr close <n>` | Close a PR |
| `gh pr diff <n>` | Show PR diff in terminal |

### 8.4 Issues

| Command | Description |
|--------|-------------|
| `gh issue create` | Create an issue |
| `gh issue list` | List open issues |
| `gh issue view <n>` | View an issue |
| `gh issue close <n>` | Close an issue |
| `gh issue comment <n> -b "message"` | Comment on an issue |

### 8.5 Actions

| Command | Description |
|--------|-------------|
| `gh run list` | List recent workflow runs |
| `gh run view <id>` | View a run's details |
| `gh run watch <id>` | Watch a run live |
| `gh run rerun <id>` | Re-run a workflow |
| `gh workflow list` | List all workflows |
| `gh workflow run <workflow>` | Manually trigger a workflow |

---

## 9. Release Management & Versioning

### 9.1 Semantic Versioning (SemVer)

```
v MAJOR . MINOR . PATCH
  │       │       │
  │       │       └── Bug fixes, no breaking changes
  │       └────────── New features, backward compatible
  └────────────────── Breaking changes
```

| Change | Version Bump | Example |
|--------|-------------|---------|
| Bug fix | PATCH | `1.2.3 → 1.2.4` |
| New feature | MINOR | `1.2.3 → 1.3.0` |
| Breaking change | MAJOR | `1.2.3 → 2.0.0` |
| Pre-release | suffix | `2.0.0-alpha.1` |
| Build metadata | suffix | `1.0.0+build.123` |

### 9.2 Automated Releases with GitHub Actions

```yaml
name: Release

on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  release:
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v4

      - name: Build
        run: npm ci && npm run build

      - name: Create GitHub Release
        uses: softprops/action-gh-release@v2
        with:
          files: dist/**
          generate_release_notes: true
```

### 9.3 Conventional Commits + Changelog

```bash
# Install standard-version or release-please
npm install --save-dev standard-version

# Bump version and generate CHANGELOG.md automatically
npx standard-version

# It reads commit messages like:
# feat: → minor bump
# fix:  → patch bump
# feat!: or BREAKING CHANGE: → major bump
```

---

## 10. Monorepo Strategies on GitHub

### 10.1 What is a Monorepo?

A single repository that contains multiple projects, packages, or services.

```
monorepo/
├── apps/
│   ├── web/
│   ├── mobile/
│   └── api/
├── packages/
│   ├── ui-components/
│   ├── utils/
│   └── config/
└── package.json
```

### 10.2 Path-Based Workflow Triggers

Only run CI for the service that actually changed:

```yaml
on:
  push:
    paths:
      - 'apps/api/**'
      - 'packages/utils/**'

jobs:
  test-api:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: cd apps/api && npm test
```

### 10.3 Popular Monorepo Tools

| Tool | Description |
|------|-------------|
| **Turborepo** | High-performance build system with caching |
| **Nx** | Smart monorepo tooling with dependency graph |
| **Lerna** | Manages versioning and publishing of packages |
| **pnpm workspaces** | Efficient package management for monorepos |
| **Changesets** | Version management and changelog generation |

---

## 11. Git Performance & Maintenance

| Command | Description | Example |
|--------|-------------|---------|
| `git gc` | Run garbage collection — pack loose objects | `git gc` |
| `git gc --aggressive` | More thorough but slower GC | `git gc --aggressive` |
| `git prune` | Remove unreachable objects | `git prune` |
| `git fsck` | Verify integrity of the object database | `git fsck` |
| `git pack-refs --all` | Pack all refs into single file | `git pack-refs --all` |
| `git repack -ad` | Repack all objects into new pack file | `git repack -ad` |
| `git maintenance start` | Enable scheduled background maintenance | `git maintenance start` |
| `git sparse-checkout init` | Enable sparse checkout (partial clone) | `git sparse-checkout init` |
| `git sparse-checkout set <dir>` | Only check out specific directories | `git sparse-checkout set src/` |
| `git clone --depth 1 <url>` | Shallow clone (latest commit only) | `git clone --depth 1 https://...` |
| `git clone --filter=blob:none <url>` | Blobless clone — skip file contents | `git clone --filter=blob:none https://...` |
| `git clone --filter=tree:0 <url>` | Treeless clone — fastest for CI | `git clone --filter=tree:0 https://...` |

---

## 12. Custom GitHub Actions

Build your own reusable Action and publish it to the Marketplace.

### 12.1 Action Types

| Type | Language | Description |
|------|----------|-------------|
| **JavaScript** | Node.js | Runs directly on runner — fastest |
| **Docker** | Any | Runs in container — most flexible |
| **Composite** | YAML | Combines multiple steps — no code needed |

### 12.2 Composite Action Example

```yaml
# .github/actions/setup-and-test/action.yml
name: 'Setup and Test'
description: 'Install dependencies and run tests'

inputs:
  node-version:
    description: 'Node.js version to use'
    required: false
    default: '20'

outputs:
  test-result:
    description: 'Test pass/fail result'
    value: ${{ steps.run-tests.outputs.result }}

runs:
  using: composite
  steps:
    - uses: actions/setup-node@v4
      with:
        node-version: ${{ inputs.node-version }}

    - name: Install
      run: npm ci
      shell: bash

    - id: run-tests
      name: Test
      run: |
        npm test && echo "result=pass" >> $GITHUB_OUTPUT
      shell: bash
```

### 12.3 JavaScript Action Structure

```
my-action/
├── action.yml        → Action metadata
├── index.js          → Entry point
├── package.json
└── node_modules/     → Must be committed (or use ncc to bundle)
```

---

## 13. GitHub API & Automation

### 13.1 REST API

```bash
# List repo issues
curl -H "Authorization: Bearer $GITHUB_TOKEN" \
  https://api.github.com/repos/owner/repo/issues

# Create an issue
curl -X POST \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title":"Bug found","body":"Details here","labels":["bug"]}' \
  https://api.github.com/repos/owner/repo/issues

# Merge a PR
curl -X PUT \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
  -d '{"merge_method":"squash"}' \
  https://api.github.com/repos/owner/repo/pulls/42/merge
```

### 13.2 GraphQL API

```bash
# Query via GraphQL
curl -X POST \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "{ viewer { login repositories(first: 5) { nodes { name } } } }"
  }' \
  https://api.github.com/graphql
```

### 13.3 Webhooks

Receive HTTP POST events from GitHub to trigger external systems.

| Event | Trigger |
|-------|---------|
| `push` | Code pushed to any branch |
| `pull_request` | PR opened, closed, merged |
| `issues` | Issue opened, labeled, closed |
| `release` | Release published |
| `workflow_run` | Actions workflow completed |
| `create` | Branch or tag created |
| `delete` | Branch or tag deleted |

```yaml
# In Actions, respond to a webhook-triggered repository_dispatch
on:
  repository_dispatch:
    types: [deploy-triggered]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Payload: ${{ github.event.client_payload.version }}"
```

---

## 14. Advanced git config

```bash
# Reuse recorded conflict resolutions automatically
git config --global rerere.enabled true

# Always rebase on pull instead of merge
git config --global pull.rebase true

# Use patience diff algorithm (better for refactors)
git config --global diff.algorithm patience

# Automatically prune remote-tracking branches on fetch
git config --global fetch.prune true

# Push only current branch by default
git config --global push.default current

# Better branch display with column layout
git config --global column.ui auto
git config --global branch.sort -committerdate

# More context in diffs
git config --global diff.context 10

# Auto-setup remote tracking on push
git config --global push.autoSetupRemote true
```

---

## 15. Key Things to Always Remember

| Rule | Why It Matters |
|------|----------------|
| Git objects are immutable | Commits are never modified — only new ones created |
| Reflog is your safety net | Almost any mistake can be recovered within 90 days |
| Shallow clones break some operations | Use full clones for development, shallow for CI |
| Signed commits prove authorship | Critical in regulated or open-source environments |
| Protect secrets at the org level | Repo-level secrets can leak across forks |
| Matrix builds catch cross-platform bugs early | Don't assume Linux behavior matches Windows/macOS |
| Monorepo path filters save CI costs | Only run what actually changed |
| Reusable workflows reduce duplication | DRY principle applies to CI/CD too |
| Webhooks enable real-time integrations | Push model is always better than polling |
| Automate releases with tags | Eliminates human error in version management |

---

*This document is part of the Linux & Developer Tools series.*
*Beginner → Intermediate → **Advanced***