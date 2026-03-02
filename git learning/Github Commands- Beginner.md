# Introduction to GitHub — Beginner

---

## 1. What is Git?

**Git** is a **version control system** — it tracks changes to your files over time so you can go back to any previous version, collaborate with others, and never lose your work.

It was created by **Linus Torvalds** (yes, the same person who created Linux) in 2005 to manage the Linux kernel source code.

> **Think of Git like a save system in a video game** — except it saves every version of your entire project, not just the latest one.

### Without Git vs With Git

| Without Git | With Git |
|-------------|----------|
| `project_final.zip` | Every change is tracked automatically |
| `project_final_v2.zip` | You can go back to any point in history |
| `project_final_ACTUAL.zip` | Multiple people can work simultaneously |
| `project_final_USE_THIS.zip` | You always know who changed what and when |

---

## 2. What is GitHub?

**GitHub** is a cloud-based platform that hosts Git repositories online. It adds collaboration features on top of Git — like pull requests, issues, code reviews, and project boards.

```
Git  =  The tool that tracks your code changes locally
GitHub  =  The website that stores your code online + collaboration features
```

### Git vs GitHub

| Feature | Git | GitHub |
|---------|-----|--------|
| What it is | Version control software | Cloud hosting platform |
| Where it runs | On your local machine | On the internet |
| Created by | Linus Torvalds (2005) | Tom Preston-Werner (2008) |
| Requires internet | ❌ No | ✅ Yes |
| Free | ✅ Yes | ✅ Yes (with paid plans) |
| Alternatives | — | GitLab, Bitbucket, Gitea |

---

## 3. Key Concepts & Terminology

| Term | What It Means |
|------|---------------|
| **Repository (Repo)** | A folder that Git is tracking — your project |
| **Commit** | A saved snapshot of your changes with a message |
| **Branch** | A parallel version of your project to work on safely |
| **Merge** | Combining changes from one branch into another |
| **Clone** | Downloading a copy of a remote repo to your machine |
| **Fork** | Your own personal copy of someone else's repo on GitHub |
| **Push** | Uploading your local commits to GitHub |
| **Pull** | Downloading latest changes from GitHub to your machine |
| **Pull Request (PR)** | A request to merge your changes into another branch |
| **Remote** | The online version of your repo (usually on GitHub) |
| **Origin** | Default name for the remote repo you cloned from |
| **Staging Area** | Where you prepare changes before committing |
| **Working Directory** | Your actual project folder with files you're editing |
| **HEAD** | Pointer to the current commit you're on |
| **.gitignore** | File that tells Git which files to ignore |
| **README.md** | The front page of your repo — shown on GitHub |

---

## 4. Installing Git

### 4.1 Installation by OS

| OS | Command / Method |
|----|-----------------|
| Ubuntu / Debian | `sudo apt install git` |
| Fedora / RHEL | `sudo dnf install git` |
| Arch Linux | `sudo pacman -S git` |
| macOS | `brew install git` or install Xcode CLT |
| Windows | Download from https://git-scm.com |

### 4.2 Verify Installation

```bash
git --version
# git version 2.43.0
```

### 4.3 First-Time Setup

```bash
# Set your name and email (used in every commit)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Set default branch name to main
git config --global init.defaultBranch main

# Set default editor (optional)
git config --global core.editor "code --wait"   # VS Code
git config --global core.editor "nano"          # Nano

# View all config
git config --list
```

---

## 5. The Git Workflow

```
Working Directory   →   Staging Area   →   Local Repo   →   GitHub (Remote)
  (edit files)          (git add)          (git commit)      (git push)
```

### How Files Move Through Git

| Stage | Description | Command |
|-------|-------------|---------|
| **Untracked** | New file Git doesn't know about yet | — |
| **Staged** | File added to staging, ready to commit | `git add` |
| **Committed** | Snapshot saved to local repo history | `git commit` |
| **Pushed** | Commit uploaded to GitHub | `git push` |

---

## 6. Core Git Commands

### 6.1 Setting Up a Repo

| Command | Description | Example |
|--------|-------------|---------|
| `git init` | Initialize a new Git repo in current folder | `git init` |
| `git clone <url>` | Clone a remote repo to your machine | `git clone https://github.com/user/repo.git` |
| `git clone <url> <folder>` | Clone into a specific folder name | `git clone https://github.com/user/repo.git myproject` |

### 6.2 Tracking Changes

| Command | Description | Example |
|--------|-------------|---------|
| `git status` | Show what's changed, staged, untracked | `git status` |
| `git add <file>` | Stage a specific file | `git add index.html` |
| `git add .` | Stage all changed files | `git add .` |
| `git add -p` | Interactively stage chunks of changes | `git add -p` |
| `git diff` | Show unstaged changes | `git diff` |
| `git diff --staged` | Show staged changes | `git diff --staged` |

### 6.3 Committing

| Command | Description | Example |
|--------|-------------|---------|
| `git commit -m "message"` | Commit staged changes with a message | `git commit -m "add login page"` |
| `git commit -am "message"` | Stage all tracked files and commit | `git commit -am "fix typo"` |
| `git commit --amend` | Edit the last commit message or add files | `git commit --amend` |

### 6.4 Viewing History

| Command | Description | Example |
|--------|-------------|---------|
| `git log` | Show full commit history | `git log` |
| `git log --oneline` | Compact one-line per commit view | `git log --oneline` |
| `git log --oneline --graph` | Visual branch graph | `git log --oneline --graph` |
| `git log -n 5` | Show last 5 commits | `git log -n 5` |
| `git show <commit>` | Show details of a specific commit | `git show a3f5c2` |
| `git blame <file>` | Show who changed each line | `git blame index.html` |

---

## 7. Branching

Branches let you work on features or fixes in isolation without affecting the main codebase.

```
main  ──●──●──●──────────────●── (merge)
              └──●──●──●──┘
              feature/login
```

### 7.1 Branch Commands

| Command | Description | Example |
|--------|-------------|---------|
| `git branch` | List all local branches | `git branch` |
| `git branch <name>` | Create a new branch | `git branch feature/login` |
| `git switch <name>` | Switch to a branch | `git switch feature/login` |
| `git switch -c <name>` | Create and switch to new branch | `git switch -c feature/login` |
| `git checkout <name>` | Switch to branch (older syntax) | `git checkout main` |
| `git checkout -b <name>` | Create and switch (older syntax) | `git checkout -b hotfix` |
| `git branch -d <name>` | Delete a branch (safe) | `git branch -d feature/login` |
| `git branch -D <name>` | Force delete a branch | `git branch -D feature/login` |
| `git branch -m <old> <new>` | Rename a branch | `git branch -m master main` |

### 7.2 Merging

| Command | Description | Example |
|--------|-------------|---------|
| `git merge <branch>` | Merge branch into current branch | `git merge feature/login` |
| `git merge --no-ff <branch>` | Merge with a merge commit always | `git merge --no-ff feature/login` |
| `git merge --abort` | Cancel a merge in progress | `git merge --abort` |

---

## 8. Working with GitHub (Remote)

### 8.1 Connecting to GitHub

| Command | Description | Example |
|--------|-------------|---------|
| `git remote -v` | List remote connections | `git remote -v` |
| `git remote add origin <url>` | Add GitHub remote | `git remote add origin https://github.com/user/repo.git` |
| `git remote remove origin` | Remove a remote | `git remote remove origin` |
| `git remote rename origin upstream` | Rename a remote | `git remote rename origin upstream` |

### 8.2 Push & Pull

| Command | Description | Example |
|--------|-------------|---------|
| `git push origin <branch>` | Push branch to GitHub | `git push origin main` |
| `git push -u origin <branch>` | Push and set upstream tracking | `git push -u origin main` |
| `git push --all` | Push all branches | `git push --all` |
| `git pull` | Fetch + merge latest changes | `git pull` |
| `git pull origin <branch>` | Pull specific branch | `git pull origin main` |
| `git fetch` | Download changes but don't merge | `git fetch` |
| `git fetch --all` | Fetch all remotes | `git fetch --all` |

---

## 9. Undoing Things

| Command | Description | Example |
|--------|-------------|---------|
| `git restore <file>` | Discard unstaged changes in a file | `git restore index.html` |
| `git restore --staged <file>` | Unstage a file (keep changes) | `git restore --staged index.html` |
| `git revert <commit>` | Create a new commit that undoes a commit | `git revert a3f5c2` |
| `git reset --soft HEAD~1` | Undo last commit, keep changes staged | `git reset --soft HEAD~1` |
| `git reset --mixed HEAD~1` | Undo last commit, keep changes unstaged | `git reset --mixed HEAD~1` |
| `git reset --hard HEAD~1` | Undo last commit and discard all changes | `git reset --hard HEAD~1` |
| `git clean -fd` | Remove untracked files and directories | `git clean -fd` |

### When to Use What

| Situation | Command |
|-----------|---------|
| Accidentally staged a file | `git restore --staged <file>` |
| Want to throw away file edits | `git restore <file>` |
| Undo last commit but keep your work | `git reset --soft HEAD~1` |
| Undo a commit that's already pushed | `git revert <commit>` |
| Nuclear — wipe everything back | `git reset --hard HEAD~1` |

---

## 10. The .gitignore File

The `.gitignore` file tells Git which files and folders to never track.

### 10.1 Common .gitignore Patterns

```gitignore
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.o
*.class

# Environment & secrets
.env
.env.local
*.pem
*.key

# OS files
.DS_Store
Thumbs.db

# IDE files
.vscode/
.idea/
*.suo

# Logs
*.log
logs/

# Python
__pycache__/
*.pyc
.venv/
```

### 10.2 .gitignore Syntax Rules

| Pattern | Meaning |
|---------|---------|
| `*.log` | Ignore all .log files |
| `build/` | Ignore the build directory |
| `!important.log` | Do NOT ignore this specific file |
| `**/logs` | Ignore logs folder anywhere in the tree |
| `doc/*.txt` | Ignore .txt files only inside /doc |
| `#` | Comment line |

---

## 11. GitHub — Key Features

### 11.1 Important GitHub Concepts

| Feature | Description |
|---------|-------------|
| **Repository** | Your project hosted on GitHub |
| **README.md** | Markdown file shown on the repo homepage |
| **Issues** | Bug reports, feature requests, discussions |
| **Pull Request** | Propose and review code changes before merging |
| **Fork** | Your own copy of someone else's repo |
| **Star** | Bookmark a repo you like (like a like button) |
| **Watch** | Get notifications for activity on a repo |
| **GitHub Actions** | CI/CD — automate tests and deployments |
| **GitHub Pages** | Host static websites directly from a repo |
| **Releases** | Tag and publish versioned software releases |
| **Wiki** | Documentation pages for your repo |

### 11.2 GitHub Account Types

| Plan | Description |
|------|-------------|
| **Free** | Unlimited public + private repos, limited Actions minutes |
| **Pro** | More Actions minutes, GitHub Pages for private repos, insights |
| **Team** | For organizations — team management, reviews |
| **Enterprise** | SSO, compliance, advanced security features |

---

## 12. A Complete Beginner Workflow

### Starting a new project from scratch

```bash
# 1. Create a folder and initialize Git
mkdir my-project
cd my-project
git init

# 2. Create your first file
echo "# My Project" > README.md

# 3. Stage and commit
git add .
git commit -m "first commit"

# 4. Create a repo on GitHub (via website), then connect it
git remote add origin https://github.com/yourusername/my-project.git
git branch -M main
git push -u origin main
```

### Contributing to an existing project

```bash
# 1. Fork the repo on GitHub (click Fork button)

# 2. Clone your fork
git clone https://github.com/yourusername/project.git
cd project

# 3. Create a new branch for your change
git switch -c fix/typo-in-readme

# 4. Make your changes, then stage and commit
git add README.md
git commit -m "fix: correct typo in README"

# 5. Push your branch to GitHub
git push origin fix/typo-in-readme

# 6. Open a Pull Request on GitHub
# Go to your fork on GitHub → Click "Compare & pull request"
```

---

## 13. Writing Good Commit Messages

A good commit message tells **what** changed and **why** — not how.

### Format

```
<type>: <short summary>

<optional longer description>
```

### Commit Types

| Type | When to Use |
|------|-------------|
| `feat` | Adding a new feature |
| `fix` | Fixing a bug |
| `docs` | Documentation changes |
| `style` | Formatting, no logic change |
| `refactor` | Code restructure, no feature/fix |
| `test` | Adding or fixing tests |
| `chore` | Build process, dependencies |
| `perf` | Performance improvement |

### Good vs Bad Examples

| ❌ Bad | ✅ Good |
|--------|--------|
| `fix stuff` | `fix: resolve null pointer on login page` |
| `changes` | `feat: add dark mode toggle to settings` |
| `update` | `docs: update README with setup instructions` |
| `wip` | `refactor: extract auth logic into middleware` |

---

## 14. SSH Authentication with GitHub

Using SSH means you never have to enter your username and password when pushing.

```bash
# Step 1 — Generate SSH key
ssh-keygen -t ed25519 -C "you@example.com"

# Step 2 — Copy your public key
cat ~/.ssh/id_ed25519.pub

# Step 3 — Add to GitHub
# GitHub → Settings → SSH and GPG keys → New SSH key → Paste

# Step 4 — Test connection
ssh -T git@github.com
# Hi username! You've successfully authenticated.

# Step 5 — Use SSH remote instead of HTTPS
git remote set-url origin git@github.com:username/repo.git
```

---

## 15. Key Things to Always Remember

| Rule | Why It Matters |
|------|----------------|
| Commit often, commit small | Easier to understand history and revert changes |
| Write meaningful commit messages | Your future self will thank you |
| Never commit secrets or passwords | Once pushed, it's in history forever |
| Always pull before you push | Avoids unnecessary merge conflicts |
| Use branches for every feature or fix | Keeps main branch stable and clean |
| Review your changes before committing | `git diff` and `git status` are your friends |
| Add a `.gitignore` at the start | Prevents junk files from ever getting in |
| `git reset --hard` is dangerous | It permanently destroys uncommitted work |

---
