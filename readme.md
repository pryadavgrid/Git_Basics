
# Git & GitHub – Developer Guide

## Introduction

**Git** is a free and open-source version control system used to track changes in files and source code. It allows developers to manage project history, collaborate efficiently, and safely revert to previous versions when issues occur. Git is available for **Windows**, **macOS**, and **Linux**, and runs locally on your computer.

Think of Git like a **checkpoint system** in a game:  
you create save points (commits), and if something breaks, you can go back to a previous stable checkpoint.

**GitHub** is a **hosting service** for Git repositories.  
Git is the software, and GitHub is the online platform that hosts Git repositories and enables collaboration over the internet.

---

## VCS (Version Control System)

A **Version Control System (VCS)** helps track file changes over time, manage multiple versions of a project, and enable collaboration among developers.

---

## Basic Git Commands

### Check Git Version
```bash
git --version
````

Displays the installed Git version.

---

### Present Working Directory

```bash
pwd
```

Shows the current directory path in the terminal.

---

### Repository Status

```bash
git status
```

Displays the current state of the repository (staged, unstaged, untracked files).

**Common error:**

```
fatal: not a git repository (or any of the parent directories): .git
```

This means the current folder is **not initialized as a Git repository**.

---

## Git Configuration

Set your global Git identity:

```bash
git config --global user.email "your-email@example.com"
git config --global user.name "Your Name"
```

---

## Initialize a Repository

```bash
git init
```

Initializes Git tracking in the current directory and creates a hidden `.git` folder.
This is the starting point of version control for a project.

---

## Git Workflow

**Flow:**

```
Write → Add → Commit → Push
```

### Steps:

1. **Initialize repository**

   ```bash
   git init
   ```

2. **Stage changes**

   ```bash
   git add
   ```

3. **Commit changes (local only)**

   ```bash
   git commit
   ```

4. **Push to GitHub (remote)**

   ```bash
   git push
   ```

> `add` and `commit` save data **locally**
> `push` sends data to **GitHub (remote repository)**

---

## Staging Files

### Add specific files

```bash
git add <FILE_NAME_1> <FILE_NAME_2>
```

### Add all files

```bash
git add .
```

---

## Commit Changes

```bash
git commit -m "Commit message"
```

* `-m` → commit message flag
* Creates a checkpoint in project history

---

## View Commit History

### Full log

```bash
git log
```

Shows:

* Commit ID (hash)
* Branch
* Author
* Date
* Commit message

---

### One-line log

```bash
git log --oneline
```

Compact commit history (one line per commit).

---

## Git Editor (VIM & VS Code)

### Default Editor: VIM

If you commit **without `-m`**, Git opens **VIM** to enter a commit message.

---

### Set VS Code as Default Git Editor

#### Step 1: Install VS Code command

* Press: `Command + Shift + P`
* Search: `Shell Command: Install 'code' command in PATH`

#### Step 2: Configure Git

```bash
git config --global core.editor "code --wait"
```

Now, when committing without `-m`, VS Code opens `COMMIT_EDITMSG`.
After writing the message and closing the file, Git automatically completes the commit.

---

## `.gitignore` File

`.gitignore` is used to exclude files/folders from tracking.

Example:

```
node_modules
.env
dist
```

### Notes:

* Git does **not track empty folders**
* To keep empty folders, add a file:

```
.gitkeep
```

---

## Branches in Git

Branches allow parallel development on different features or fixes.

### HEAD

`HEAD` is a pointer to the current branch and latest commit you are working on.

> Default branch used to be `master`
> Now conventionally named `main`

---

## Branch Commands

### List branches

```bash
git branch
```

### Create branch

```bash
git branch bug-fix
```

### Switch branch

```bash
git switch bug-fix
```

### Create + switch branch

```bash
git switch -c dark-mode
```

### Checkout (older command)

```bash
git checkout orange-mode
```

---

## Merging Branches

Merging brings changes from one branch into another.

### Types of merges:

### 1. Fast-Forward Merge

Occurs when branches **have not diverged**.
No conflicts, simple history move forward.

```bash
git checkout main
git merge bug-fix
```

---

### 2. 3-Way Merge

Occurs when branches **have diverged**.
Git uses:

* Common ancestor
* Tip of branch A
* Tip of branch B

Creates a **merge commit**.

```bash
git checkout main
git merge bug-fix
```

### Difference from fast-forward:

* Fast-forward → no conflicts
* 3-way merge → possible conflicts (manual resolution required)

---

## Merge Conflicts

Example conflict markers:

```text
<<<<<<< HEAD
current branch code
=======
code from another branch
>>>>>>> bug-fix
```

You must manually resolve conflicts and choose what to keep.
VS Code provides a built-in merge conflict resolution tool.

---

## Branch Management

### Rename a branch

```bash
git branch -m <old-branch-name> <new-branch-name>
```

### Delete a branch

```bash
git branch -d <branch-name>
```

### Checkout a branch

```bash
git checkout <branch-name>
```

### List all branches

```bash
git branch
```

---

## Summary

Git provides:

* Version tracking
* History management
* Collaboration
* Safe rollback
* Parallel development
* Branching and merging workflows

GitHub provides:

* Online hosting
* Collaboration tools
* CI/CD integration
* Pull requests
* Project visibility

---

## Developer Notes

* Git = Software
* GitHub = Hosting service
* Commits = Checkpoints
* Branches = Parallel development
* Merge = Combine work
* Conflicts = Manual resolution

---




### Diff, Stash and Tags

## Git diff
The git diff is an informative command that shows the differences between two commits. It is used to compare the changes made in one commit with the changes made in another commit.
when we are staging area mean when we make changes in a file then we check before commit 
git diff --staged

# How to Read the Diff Output

* a/ - indicate original file
* b/ - indicate updated file
* --- - mark the original file
* +++ - mark the updated file
* @@ - shows the line numbers and position of changes


Example :
diff --git a/01_file.text b/01_file.text
index 2c89356..2609bf1 100644
--- a/01_file.text
+++ b/01_file.text
@@ -1,3 +1,5 @@
 This Is First File
 
-we check for that
\ No newline at end of file
+we check for that
+
+this is change for the check working of "git diff --staged" command, it compare file in staging area
\ No newline at end of file


# we can check the difference/Comparision B/W two banch, commit

# Comparing Two Branches 
git diff <FIRST-BRANCH-NAME> <SECOND-BRANCH-NAME>
Or
git diff FIRST-BRANCH-NAME..SECOND-BRANCH-NAME

Comparing Specific Commits:
git diff <commit-hash-one_or_commit-id> <commit-hash-two_or_commit-id>

### Git Stash
git stash is a was of save changes in temprory location, 
it is usefull when we want to swith one branch to second branch without using commit or add file
without using the "git stash" we can't swich one branch to another branch

Example 
there is a changes in 01_file on main branch, 
then we want to switch/checkout bug-fix branch. we use "git checkout bug-fix"
error: Your local changes to the following files would be overwritten by checkout:
         02_file.text
         Please commit your changes or stash them before you switch branches.
         Aborting

so on this situation first we use "git stash" command for the save changes in temprory location
we can give a message on stash eg. "git stash "Save this ABC"
a message see in terminal : Saved working directory and index state WIP on main: 7e45c6e merge-conflict-done


## View the stash list
You can view the list of stashes by using the following command:

git stash list


## Apply the Most Recent Stash
You can apply the stash by using the following command:

git stash apply


### Apply Specific Stash
You can apply the specific stash by using the following command:

git stash apply stash@{0}

Here stash@{0} is the name of the stash. You can use the git stash list command to get the name of the stash.

## Applying and Drop a Stash
You can apply and drop the stash by using the following command:

git stash pop


## Drop the stash
You can drop the stash by using the following command:

git stash drop


## Applying stash to a specific branch
You can apply the stash to a specific branch by using the following command:

git stash apply stash@{0} <branch-name>

## Clearing the stash
You can clear the stash by using the following command:

git stash clear


## Git Tag
it look like a sticky note, mainly this is use for relesing version like 



## Rebase
in the rebase mainly we change the head pointer of another branch
Note : most of the case rebase use in another branch not the main branch
step : 1. go to the another branch and then write comment 
git rebase main


### Resolve any conflicts
If there are any conflicts, you will need to resolve them manually. You can use the merge tool in VSCode to resolve the conflicts.

git add <resolved-files>
git rebase --continue

### Git reflog
git reflog same as git log or git log --oneline but it return more information of commit it mean git return history of commit or log

git reflog


### Find specific commit
we can find the specific history of any commit using commit HAS or Commit id

git reflog <commit-hash>


### Recover lost commits or changes

some time after push the code or commite the message we want to get back to previous branch mean some time we don't need of updated code then we want to back to previous commit then we use the reset commit
for this we need to privious branch hash where we want to go
after that we can run command

git reset --hard <commit-hash>

we can give a head vale where we want to say that how many commit we want to go back.
using command  HEAD@{1} inside the @{} we give a number where we want to roll back

git reset --hard HEAD@{1}

### GIT SSH Configuration
you can read GitHub Documentation on  **https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account**


## GitHub Set 
1. create GitHub Repo
2. in your Mac open terminal run these command 
   1. git init
   2. git add .
   3. git commit -m "COMMIT-MESSAGE"
   4. git branch -M Main 
   5. git remote -v 
   6. git git remote add origin "URL_Of_REPO"
   7. git push -u origin main

   // init initilize the repo
   // add all file
   // commit the message
   // rename tha main branch
   // check the push and fetsh bonding 
   // origin -> set the GITHUB_URL_NAME as origin it mean we do not write again and again "URL_OF_REPO" wite only origin
   // -u -> set the upstrem branch mean whenever we push the code in this repo then automatic push/pull on the upstrem branch and the next time when we use command command "git push" then automatic push the code in origin main branch.