# Git Cheat Sheet

## 1. Git configuration

### Git config
Get and set configuration variables that control all facets of how Git looks and operates.

**Set the name:**
```bash
git config --global user.name "User name"
```

**Set the email:**
```bash
git config --global user.email "xyz@gmail.com"
```

**Set the default editor:**
```bash
git config --global core.editor Vim
```

**Check the setting:**
```bash
git config -list
```

### Git alias
Set up an alias for each command:

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

---

## 2. Starting a project

### Git init
Create a local repository

```bash
git init <Repo Name>
```

### Git clone
Make a local copy of the server repository.

```bash
git clone <remote Url>
```

---

## 3. Local changes

### Git add
Add a file to staging (Index) area

```bash
git add Filename
```

Add all files of a repo to staging (Index) area

```bash
git add *
```

### Git commit
Record or snapshot the file permanently in the version history with a message

```bash
git commit -m "Commit Message"
```

---

## 4. Track changes

### Git diff

Track the changes that have not been staged:
```bash
git diff
```

Track the changes that have staged but not committed:
```bash
git diff --staged
```

Track the changes after committing a file:
```bash
git diff HEAD
```

Track the changes between two commits:
```bash
git diff <commit1-sha> <commit2-sha>
```

Git Diff Branches:
```bash
git diff <branch 1> <branch 2>
```

### Git status
Display the state of the working directory and the staging area.

```bash
git status
```

### Git show
Shows objects:

```bash
git show <options> <objects>
```

---

## 5. Commit History

### Git log

Display the most recent commits and the status of the head:
```bash
git log
```

Display the output as one commit per line:
```bash
git log --oneline
```

Displays the files that have been modified:
```bash
git log --stat
```

Display the modified files with location:
```bash
git log -p
```

### Git blame
Display the modification on each line of a file:

```bash
git blame <file name>
```

---

## 6. Ignoring files

### .gitignore
Specify intentionally untracked files that Git should ignore.

Create .gitignore:
```bash
touch .gitignore
```

List the ignored files:
```bash
git ls-files -i --exclude-standard
```

---

## 7. Branching

### Git branch

Create branch:
```bash
git branch <branch name>
```

List Branch:
```bash
git branch --list
```

Delete Branch:
```bash
git branch -d <branch name>
```

Delete a remote Branch:
```bash
git push origin -delete <branch name>
```

Rename Branch:
```bash
git branch -m <old branch name><new branch name>
```

### Git checkout

Switch between branches in a repository.

Switch to a particular branch:
```bash
git checkout <branch name>
```

Create a new branch and switch to it:
```bash
git checkout -b <branchname>
```

Checkout a Remote branch:
```bash
git checkout <remotebranch>
```

### Git stash

Switch branches without committing the current branch.

Stash current work:
```bash
git stash
```

Saving stashes with a message:
```bash
git stash save "<Stashing Message>"
```

Check the stored stashes:
```bash
git stash list
```

Re-apply the changes that you just stashed:
```bash
git stash apply
```

Track the stashes and their changes:
```bash
git stash show
```

Re-apply the previous commits:
```bash
git stash pop
```

Delete a most recent stash from the queue:
```bash
git stash drop
```

Delete all the available stashes at once:
```bash
git stash clear
```

Stash work on a separate branch:
```bash
git stash branch <branch name>
```

### Git cherry-pick
Apply the changes introduced by some existing commit:

```bash
git cherry-pick <commit id>
```

---

## 8. Merging

### Git merge

Merge the branches:
```bash
git merge <branch name>
```

Merge the specified commit to currently active branch:
```bash
git merge <commit>
```

### Git rebase
Apply a sequence of commits from distinct branches into a final commit.

```bash
git rebase <branch name>
```

Continue the rebasing process:
```bash
git rebase --continue
```

Abort the rebasing process:
```bash
git rebase --skip
```

### Git interactive rebase
Allow various operations like edit, rewrite, reorder, and more on existing commits.

```bash
git rebase -i
```

---

## 9. Remote

### Git remote

Check the configuration of the remote server:
```bash
git remote -v
```

Add a remote for the repository:
```bash
git remote add <short name> <remote URL>
```

Fetch the data from remote server:
```bash
git fetch <Remote>
```

Remove a remote connection from the repository:
```bash
git remote rm <destination>
```

Rename remote server:
```bash
git remote rename <old name> <new name>
```

Show additional information about a particular remote:
```bash
git remote show <remote>
```

Change remote:
```bash
git remote set-url <remote name> <newURL>
```

### Git origin master

Push data to remote server:
```bash
git push origin master
```

Pull data from remote server:
```bash
git pull origin master
```

---

## 10. Pushing Updates

### Git push
Transfer the commits from your local repository to a remote server.

Push data to remote server:
```bash
git push origin master
```

Force push data:
```bash
git push <remote> <branch> -f
```

Delete a remote branch by push command:
```bash
git push origin -delete edited
```

---

## 11. Pulling updates

### Git pull
Pull the data from the server:
```bash
git pull origin master
```

Pull a remote branch:
```bash
git pull <remote branch URL>
```

### Git fetch
Downloads branches and tags from one or more repositories.

Fetch the remote repository:
```bash
git fetch <repository Url>
```

Fetch a specific branch:
```bash
git fetch <branch URL> <branch name>
```

Fetch all the branches simultaneously:
```bash
git fetch --all
```

Synchronize the local repository:
```bash
git fetch origin
```

---

## 12. Undo changes

### Git revert
Undo the changes

```bash
git revert
```

Revert a particular commit:
```bash
git revert <commit-ish>
```

### Git reset
Reset the changes:

```bash
git reset --hard
git reset --soft
git reset --mixed
```

---

## 13. Removing files

### Git rm
Remove the files from the working tree and from the index:

```bash
git rm <file Name>
```

Remove files from Git but keep the files in your local repository:

```bash
git rm --cached <file Name>
```
