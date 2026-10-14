t is Git?

Git is a **Version Control System (VCS)** used to track changes in files and code.

In simple words, Git helps us record changes, go back to previous versions, and collaborate with other developers.

**Example:**

Imagine you are developing a website.

- Day 1: You create a login page.
- Day 2: You add a signup page.
- Day 3: You modify the login page, but something breaks.

Git helps you track these changes and recover earlier versions when needed.

## 2. Why do we use Git?

- **Track changes:** Know what changed in your code.
- **Save versions:** Record changes using commits.
- **Undo mistakes:** Restore or reverse unwanted changes.
- **Work in teams:** Share code with other developers.
- **Use branches:** Develop features separately without directly changing the main branch.

## 3. Git vs GitHub

| Git | GitHub |
| --- | --- |
| A version control system | An online platform for hosting Git repositories |
| Works locally on your computer | Stores repositories remotely |
| Tracks file changes and commits | Helps teams share code and collaborate |
| Can work without internet | Requires internet for most remote operations |

**Remember:** Git is the tool. GitHub is a platform that hosts Git repositories.

Other Git hosting platforms include GitLab and Bitbucket.

## 4. Important Git Terminology

**Repository (Repo)**

A project tracked by Git. It contains project files and Git history.

**Commit**

A saved snapshot of changes in your repository.

**Branch**

An independent line of development. It lets you work on a feature without directly modifying another branch.

**Working Directory**

The files you are currently working on.

**Staging Area**

The place where you select changes to include in your next commit.

**Remote Repository**

A repository hosted somewhere else, such as GitHub, that you can share and synchronize with.

## 5. The Three Main Areas in Git

Git tracks your work through three important areas.

```
Working Directory
       ↓
  git add
       ↓
  Staging Area
       ↓
  git commit
       ↓
Local Repository
```

### A. Working Directory

Where you create, edit, and delete project files.

Example: You modify `main.py`.

### B. Staging Area

Where you select which changes should be included in the next commit.

```
git add main.py
```

This stages the changes in `main.py`.

### C. Local Repository

Where Git records commits and maintains your project history.

```
git commit -m "Add login functionality"
```

This creates a commit containing the staged changes.

**Easy way to remember:**

- Working Directory = Modify
- Staging Area = Select
- Local Repository = Save a commit

## 6. Basic Git Commands

### Step 1: Check Git version

```
git --version
```

Shows the installed Git version.

### Step 2: Configure your identity

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Git uses this information to identify the author of your commits.

### Step 3: Create a repository

```
git init
```

Initializes a new Git repository in the current directory.

### Step 4: Check repository status

```
git status
```

Shows which files are untracked, modified, staged, or otherwise have changes.

### Step 5: Stage changes

```
git add main.py
```

Stages changes in a specific file.

To stage all changes in the current directory:

```
git add .
```

### Step 6: Commit changes

```
git commit -m "Initial commit"
```

Records the staged changes in the local repository.

### Step 7: View commit history

```
git log
```

Shows commit history, including commit IDs, authors, dates, and messages.

For a compact view:

```
git log --oneline
```

## 7. What is a Git Workflow?

A Git workflow is the sequence of steps we follow while working on code.

Example:

```
Create or modify files
        ↓
Check changes
        ↓
git status
        ↓
Stage changes
        ↓
git add .
        ↓
Commit changes
        ↓
git commit -m "message"
```

This saves your changes as a commit in your local repository.

**Important:** A commit is saved locally. It does not automatically upload your code to GitHub.

## 8. What is a Remote Repository?

A remote repository is a version of your repository hosted elsewhere, usually on a server or platform such as GitHub.

We use remote repositories to share code and synchronize work between local and remote copies.

### Important commands

Check configured remotes:

```
git remote -v
```

Connect a local repository to a remote:

```
git remote add origin <repository-url>
```

Push local commits to a remote branch:

```
git push origin main
```

Download and integrate remote changes into your current branch:

```
git pull
```

**Remember:**

- `git add` → Stage changes.
- `git commit` → Save changes locally.
- `git push` → Send commits to a remote.
- `git pull` → Fetch and integrate remote changes.

## 9. Quick Revision

| Command | Purpose |
| --- | --- |
| `git --version` | Check Git version |
| `git config` | Configure Git settings |
| `git init` | Initialize a repository |
| `git status` | Check current changes |
| `git add` | Stage changes |
| `git commit` | Save staged changes as a commit |
| `git log` | View commit history |
| `git remote -v` | View remote repositories |
| `git push` | Send commits to a remote |
| `git pull` | Fetch and integrate remote changes |

## 10. Interview Revision

**What is Git?**

Git is a distributed version control system used to track code changes and manage project history.

**What is a repository?**

A repository stores project files tracked by Git along with their history.

**What is a commit?**

A commit records a snapshot of the staged changes.

**Why do we use `git add`?**

To select changes for the next commit.

**What is the difference between `git add` and `git commit`?**

`git add` stages changes, whereas `git commit` records the staged changes in the local repository.

**What is the difference between `git commit` and `git push`?**

`git commit` saves changes locally. `git push` sends commits to a remote repository.

**What is a branch?**

A branch is an independent line of development used to work on changes separately.

---

# 2. Git Branching & Merging

## 1. What is a Branch?

A branch is an independent line of development in Git.

It allows developers to work on new features or bug fixes without directly changing another branch.

**Example:**

You have a website running on `main`. Now you want to develop a login feature.

Instead of making all changes directly on `main`, you create a separate branch called `feature-login`.

```
main
  \
   feature-login
```

You can develop and test the login feature separately.

## 2. Why Do We Use Branches?

- Develop new features separately.
- Fix bugs without disturbing ongoing development.
- Allow multiple developers to work in parallel.
- Test changes before merging them into the main codebase.
- Keep the main branch more stable.

## 3. Important Branch Commands

### A. View branches

```
git branch
```

Shows your local branches.

The `*` symbol indicates the branch you are currently on.

### B. Create a branch

```
git branch feature-login
```

Creates a new branch called `feature-login`.

**Important:** This command creates the branch but does not switch to it.

### C. Switch to a branch

```
git switch feature-login
```

Switches to the existing `feature-login` branch.

### D. Create and switch to a branch

```
git switch -c feature-login
```

Creates the branch and switches to it in one command.

### E. Rename a branch

```
git branch -m new-branch-name
```

Renames the current branch.

### F. Delete a branch

```
git branch -d feature-login
```

Deletes a local branch if Git considers it safely merged.

To force-delete a local branch:

```
git branch -D feature-login
```

**Warning:** Force deletion can discard branch-only commits from normal branch references.

## 4. What Is Merging?

Merging combines changes from one branch into another.

**Example:** You developed a login feature on `feature-login`. Now you want to bring those changes into `main`.

### Step 1: Switch to the target branch

```
git switch main
```

### Step 2: Merge the feature branch

```
git merge feature-login
```

Git attempts to integrate the changes from `feature-login` into `main`.

**Remember:** Switch to the branch that should receive the changes, then run `git merge`.

### Example workflow

```
main:           A → B → E
                     ↗
feature-login: A → B → C → D
```

After merging, the changes from the feature branch are integrated into `main`. The exact commit graph depends on whether Git performs a fast-forward merge or creates a merge commit.

## 5. Types of Merge

### A. Fast-forward merge

A fast-forward merge happens when the target branch has no new commits that diverge from the branch being merged.

Git simply moves the target branch forward.

```
Before:

main:    A → B
              \
feature:       C → D

After:

main:    A → B → C → D
```

No separate merge commit is required.

### B. Three-way merge

A three-way merge is used when both branches have diverged from a common ancestor.

Git combines the changes and normally creates a merge commit.

```
          C → D  (feature)
         /       \
A → B             M  (merge commit)
         \       /
          E → F  (main)
```

This example illustrates the idea of two branches having their own commits before merging.

## 6. What Is a Merge Conflict?

A merge conflict happens when Git cannot automatically reconcile changes from different branches.

For example, both branches modify the same lines of a file differently.

Git may show conflict markers like these:

```
<<<<<<< HEAD
Hello from main
=======
Hello from feature
>>>>>>> feature
```

### How to resolve a conflict

1. Open the file containing the conflict.
2. Decide which changes to keep, or combine both.
3. Remove the conflict markers.
4. Stage the resolved file.
5. Complete the merge commit if Git requires it.

Commands:

```
git status
git add <file-name>
git commit
```

For a merge in progress, `git commit` completes the merge when a merge commit is needed.

To cancel a merge that has not been completed:

```
git merge --abort
```

Use this when you want to return to the pre-merge state and Git can restore it safely.

## 7. Local Branch vs Remote Branch

A local branch exists in your local repository.

A remote-tracking branch represents the last known state of a branch on a remote repository.

Example:

```
main          → Local branch
origin/main   → Remote-tracking branch
```

Useful commands:

```
git branch
```

Lists local branches.

```
git branch -r
```

Lists remote-tracking branches.

```
git branch -a
```

Lists local and remote-tracking branches.

To publish a new local branch to GitHub:

```
git push -u origin feature-login
```

The `-u` option sets the upstream relationship, making future pushes and pulls on that branch easier.

## 8. Quick Revision

| Command | Purpose |
| --- | --- |
| `git branch` | List local branches |
| `git branch feature-login` | Create a branch |
| `git switch feature-login` | Switch branches |
| `git switch -c feature-login` | Create and switch |
| `git branch -m new-name` | Rename the current branch |
| `git branch -d feature-login` | Delete a safely merged local branch |
| `git merge feature-login` | Merge into the current branch |
| `git merge --abort` | Abort an unfinished merge |
| `git branch -r` | List remote-tracking branches |
| `git push -u origin feature-login` | Publish a branch and set its upstream |

## 9. Interview Revision

**What is a Git branch?**

A branch is an independent line of development used to work on changes separately.

**What is merging?**

Merging integrates changes from one branch into another.

**What is a merge conflict?**

A merge conflict occurs when Git cannot automatically reconcile changes between branches.

**What is the difference between `git branch` and `git switch`?**

`git branch` manages or lists branches. `git switch` changes the current branch or creates and switches to a branch with `-c`.

**What is the difference between fast-forward and three-way merge?**

A fast-forward merge moves the target branch forward when its history allows it. A three-way merge combines diverged histories and normally creates a merge commit.

**Which branch receives the merge?**

The branch you are currently on when you execute `git merge`.

---

# 3. Git Remote Operations

## 1. What Is a Remote Repository?

A remote repository is a Git repository hosted on another system or platform, such as GitHub.

Developers use remote repositories to share code and collaborate with their team.

**Example:**

- Local repository → Code on your computer.
- Remote repository → Code hosted on GitHub.

```
Your Computer                    GitHub
┌─────────────────┐             ┌─────────────────┐
│ Local Repository│  ────────→  │Remote Repository│
│                 │  ←────────  │                 │
└─────────────────┘             └─────────────────┘
```

## 2. What Is `origin`?

`origin` is the default name commonly given to a remote repository.

Example:

```
git remote -v
```

Output:

```
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```

Here:

- `origin` → Remote name.
- URL → Address of the remote repository.
- `fetch` → Used to retrieve information and objects from the remote.
- `push` → Used to send commits to the remote.

**Remember:** `origin` is just a name. It is not a special Git command or a GitHub account.

## 3. Important Git Remote Commands

### A. `git clone`

**Purpose:** Copy an existing remote repository to your computer.

```
git clone https://github.com/user/project.git
```

Git creates a local copy of the repository, including its available history and default remote configuration.

**When to use it?**

When you want to start working on an existing project.

### B. `git remote -v`

**Purpose:** View configured remote repositories.

```
git remote -v
```

Shows the remote names and their URLs.

### C. `git remote add`

**Purpose:** Connect your local repository to a remote repository.

```
git remote add origin https://github.com/user/project.git
```

Use this when you already have a local Git repository and want to connect it to GitHub.

### D. `git push`

**Purpose:** Send your local commits to a remote repository.

```
git push origin main
```

Here:

- `origin` → Remote repository name.
- `main` → Branch to push.

**Remember:** Push sends commits, not simply every uncommitted file change.

### E. `git fetch`

**Purpose:** Download new commits and other relevant information from a remote without integrating them into your current branch.

```
git fetch origin
```

After fetching, you can inspect what changed before deciding how to integrate it.

**Remember:** Fetch = Download remote updates without merging them into your current branch.

### F. `git pull`

**Purpose:** Fetch remote updates and integrate them into your current branch.

```
git pull origin main
```

This fetches from the remote `main` branch and integrates its changes into your current branch.

Depending on your Git configuration, integration may use a merge or rebase.

**Remember:** Pull = Fetch + Integrate.

## 4. Difference Between Fetch and Pull

| `git fetch` | `git pull` |
| --- | --- |
| Downloads remote updates | Downloads and integrates remote updates |
| Does not update your current branch through integration | Updates your current branch through integration |
| Useful for checking changes first | Useful when you want to integrate remote changes |

**Example:**

Suppose another developer pushes new code to GitHub.

With fetch:

```
git fetch origin
git log --oneline main..origin/main
```

This displays commits present on `origin/main` but not on your local `main` branch.

With pull:

```
git pull origin main
```

Git fetches the remote changes and attempts to integrate them into your current branch.

## 5. What Is an Upstream Branch?

An upstream branch is the remote-tracking branch associated with your local branch for operations such as `git pull` and `git push`.

Example:

```
git push -u origin feature-login
```

The `-u` option sets the upstream relationship.

After this, you can usually use:

```
git push
git pull
```

without specifying the remote and branch each time.

## 6. Complete GitHub Workflow

Suppose you are working on a project and want to push your changes.

### Step 1: Check your current branch

```
git branch
```

### Step 2: Check your changes

```
git status
```

### Step 3: Stage your changes

```
git add .
```

### Step 4: Commit your changes

```
git commit -m "Add login feature"
```

### Step 5: Push your commits

```
git push origin main
```

Your committed changes are sent to the remote `main` branch, assuming the push is allowed.

### Workflow to get your teammates' latest changes

```
git fetch origin
git pull origin main
```

These are two alternative ways to work with remote updates: fetch to inspect first, or pull to fetch and integrate directly. You normally do not need to run both consecutively.

## 7. Quick Revision

| Command | Purpose |
| --- | --- |
| `git clone <url>` | Copy an existing repository locally |
| `git remote -v` | View remote URLs |
| `git remote add origin <url>` | Add a remote |
| `git push origin main` | Push commits to the remote branch |
| `git fetch origin` | Download remote updates without integrating |
| `git pull origin main` | Fetch and integrate remote changes |
| `git push -u origin main` | Push and set upstream |

## 8. Interview Revision

**What is a remote repository?**

A repository hosted on another system or platform that can be used to share and synchronize code.

**What is `origin`?**

A commonly used default name for a remote repository.

**What is the difference between clone and pull?**

Clone creates a local copy of a repository. Pull fetches remote updates and integrates them into the current branch.

**What is the difference between fetch and pull?**

Fetch downloads remote updates without integrating them into the current branch. Pull fetches and integrates those updates.

**What is the difference between commit and push?**

Commit records changes locally. Push sends commits to a remote repository.

**What does `-u` do in `git push -u origin main`?**

It sets the upstream tracking relationship for the local branch.

---

# 4. Git Reset, Revert, Stash & Cherry-pick

## 1. Introduction

Git provides commands to undo commits, temporarily save unfinished work, and move specific changes between branches.

In this topic, we will learn four commands:

- `git reset`
- `git revert`
- `git stash`
- `git cherry-pick`

## 2. Git Reset

**Purpose:** Move the current branch back to an earlier commit.

Suppose your commit history looks like this:

```
A → B → C (HEAD)
```

You want to undo the latest commit, `C`.

### A. `git reset --soft`

```
git reset --soft HEAD~1
```

**What happens?**

- Moves the current branch back by one commit.
- Keeps the changes from that commit in the Staging Area.

**Remember:** Commit removed from current branch history; changes remain staged.

### B. `git reset --mixed`

```
git reset --mixed HEAD~1
```

**What happens?**

- Moves the current branch back by one commit.
- Keeps the changes in the Working Directory.
- Makes those changes unstaged.

**Remember:** Commit removed from current branch history; changes remain unstaged.

Note: `git reset HEAD~1` uses `--mixed` by default.

### C. `git reset --hard`

```
git reset --hard HEAD~1
```

**What happens?**

- Moves the current branch back by one commit.
- Discards affected tracked changes from the index and Working Directory.

**Remember:** Commit removed from the current branch history; affected tracked changes are discarded.

⚠️ Be careful! Changes discarded by `--hard` may be difficult to recover.

### Reset Quick Revision

| Command | Result |
| --- | --- |
| `--soft` | Changes stay staged |
| `--mixed` | Changes stay unstaged |
| `--hard` | Affected tracked changes are discarded |

**Important:** Reset changes the current branch history. Be cautious when working with commits already shared with others.

## 3. Git Revert

**Purpose:** Undo the changes introduced by a commit by creating a new commit.

```
git revert <commit-hash>
```

Example:

```
git revert a1b2c3d
```

Suppose your history is:

```
A → B → C → D
```

You discover that commit `C` introduced a bug.

Git creates a new commit that reverses the changes introduced by `C`.

```
A → B → C → D → E
                    ↑
              New revert commit
```

The original commit remains in history.

**When to use it?**

- When you want to undo a commit that has already been pushed.
- When working on a shared branch where rewriting history should be avoided.

**Remember:** Revert = Undo changes by creating a new commit.

## 4. Git Stash

**Purpose:** Temporarily save uncommitted changes without creating a commit.

### Example situation

You are working on a login feature, but your manager asks you to fix an urgent bug on another branch.

Your current work is unfinished, so you don't want to commit it yet.

You can use `git stash`.

### Important stash commands

Save changes:

```
git stash
```

Save changes with a description:

```
git stash push -m "Login feature work"
```

View saved stashes:

```
git stash list
```

Restore changes and remove that stash entry:

```
git stash pop
```

Restore changes but keep the stash entry:

```
git stash apply
```

Delete a stash entry:

```
git stash drop stash@{0}
```

### Stash Quick Revision

| Command | Purpose |
| --- | --- |
| `git stash` | Temporarily save changes |
| `git stash list` | View saved stashes |
| `git stash pop` | Restore and remove the stash entry |
| `git stash apply` | Restore but keep the stash entry |
| `git stash drop` | Delete a stash entry |

By default, untracked files are not included. Use `git stash -u` to include them.

**Remember:** Stash = Temporarily save unfinished work.

## 5. Git Cherry-pick

**Purpose:** Apply the changes introduced by a specific commit to your current branch.

### Example situation

You have two branches:

```
main:     A → B → C

feature:  A → B → D → E
```

Commit `E` contains an important bug fix.

You want that fix in `main`, but you don't want to merge the entire feature branch.

### Step 1: Switch to the target branch

```
git switch main
```

### Step 2: Cherry-pick the required commit

```
git cherry-pick <commit-hash>
```

Git applies the selected commit's changes and creates a new commit on `main`.

**Remember:** Cherry-pick = Apply one specific commit to your current branch.

If a conflict occurs, resolve it, stage the resolved files, and continue:

```
git add <file-name>
git cherry-pick --continue
```

To cancel an unfinished cherry-pick:

```
git cherry-pick --abort
```

## 6. Difference Between Reset, Revert, Stash & Cherry-pick

| Command | Main purpose |
| --- | --- |
| `git reset` | Move the current branch to an earlier commit |
| `git revert` | Undo a commit by creating a new commit |
| `git stash` | Temporarily save uncommitted changes |
| `git cherry-pick` | Apply a specific commit to the current branch |

## 7. Which Command Should I Use?

**Situation 1:** You committed too early and want to keep the changes staged.

Use:

```
git reset --soft HEAD~1
```

**Situation 2:** You pushed a faulty commit to a shared branch.

Usually use:

```
git revert <commit-hash>
```

**Situation 3:** You have unfinished work and need to switch branches.

Use:

```
git stash
```

**Situation 4:** You need one bug fix from another branch.

Use:

```
git cherry-pick <commit-hash>
```

## 8. Interview Revision

**What is the difference between reset and revert?**

Reset moves the current branch reference to an earlier commit. Revert creates a new commit that reverses changes from an earlier commit.

**What is the difference between `--soft` and `--mixed`?**

Soft keeps the changes staged. Mixed keeps the changes unstaged.

**What is Git stash?**

It temporarily saves uncommitted changes so you can work on something else.

**What is cherry-pick?**

It applies a specific commit's changes to the current branch.

**Is reset safe for shared history?**

Reset can rewrite branch history. Revert is generally safer when undoing changes on shared branches.

---

*CI/CD*
