# 🧑‍💻 GitHub Collaboration Guide for Students

> A practical guide to working with Git and GitHub in a team environment — covering branching, pull requests, Kanban, Agile basics, and real collaboration workflows.

---

## 📚 Recommended Reading Before You Start

These are beginner-friendly, well-structured resources. Go through at least one before diving in:

1. 🔗 [**Pro Git Book (free, official)**](https://git-scm.com/book/en/v2) — The definitive Git reference. Chapters 1–3 are essential.
2. 🔗 [**GitHub Skills (interactive labs)**](https://skills.github.com/) — Hands-on exercises directly in GitHub. Best way to learn by doing.
3. 🔗 [**Atlassian Git Tutorials**](https://www.atlassian.com/git/tutorials) — Clean, visual explanations of every Git concept. Great for branching and merging.
4. 🔗 [**Oh My Git! (game)**](https://ohmygit.org/) — A visual card-based game that teaches Git commands interactively. Surprisingly effective.

---

## 🍴 How to Fork a Repository

Forking creates your own personal copy of someone else's repository under your GitHub account.

**When to fork:** When you don't have write access to the original repo (e.g., open-source projects or a teacher's template repo).

### Steps:

1. Go to the repository page on GitHub.
2. Click the **Fork** button in the top-right corner.
3. Select your account as the destination.
4. GitHub creates a copy at `https://github.com/YOUR_USERNAME/REPO_NAME`.
5. Clone your fork locally:

```bash
git clone https://github.com/YOUR_USERNAME/REPO_NAME.git
cd REPO_NAME
```

6. Add the original repo as `upstream` so you can pull future updates:

```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/REPO_NAME.git
```

7. Verify your remotes:

```bash
git remote -v
# origin    https://github.com/YOUR_USERNAME/REPO_NAME.git (fetch)
# upstream  https://github.com/ORIGINAL_OWNER/REPO_NAME.git (fetch)
```

> 💡 **Tip:** `origin` = your fork. `upstream` = the original repo.

---

## 👥 How to Add Collaborators

Collaborators have direct push access to your repository — no forking needed.

**When to use:** In team projects where everyone works on the same repo.

### Steps:

1. Go to your repository on GitHub.
2. Click **Settings** (top menu of the repo).
3. In the left sidebar, click **Collaborators** (under "Access").
4. Click **Add people**.
5. Search by GitHub username or email.
6. Select the correct person and click **Add [username] to this repository**.
7. The person receives an email invitation — they must **accept** it before they can push.

> ⚠️ Only the repository owner can add collaborators. If you're working in a GitHub Organization, this is done via **Teams** instead.

---

## 🌿 How to Create and Name a Branch

Branches let you work on a feature or fix without touching the main codebase.

### Creating a branch:

```bash
# Make sure you're up to date first
git checkout main
git pull origin main

# Create and switch to a new branch
git checkout -b your-branch-name

# Or with newer Git versions:
git switch -c your-branch-name
```

### Branch Naming Conventions

Good branch names are short, lowercase, and use hyphens. They should describe **what the branch does**.

| Type | Pattern | Example |
|------|---------|---------|
| New feature | `feat/description` | `feat/user-login` |
| Bug fix | `fix/description` | `fix/navbar-overflow` |
| Documentation | `docs/description` | `docs/update-readme` |
| Refactor | `refactor/description` | `refactor/auth-module` |
| Chore / config | `chore/description` | `chore/update-dependencies` |
| Testing | `test/description` | `test/login-unit-tests` |

> ❌ Bad: `my-branch`, `test1`, `johns-stuff`
> ✅ Good: `feat/profile-page`, `fix/broken-api-call`

---

## ✍️ How to Name Commits

Good commit messages make your project history readable and your team happy.

### The Conventional Commits standard:

```
<type>(<scope>): <short description>
```

- **type** — what kind of change (see table below)
- **scope** — optional, the part of the codebase affected (e.g., `auth`, `ui`, `api`)
- **short description** — present tense, lowercase, no period at the end

### Commit Types:

| Type | When to use |
|------|------------|
| `feat` | Adding a new feature |
| `fix` | Fixing a bug |
| `docs` | Documentation changes only |
| `style` | Formatting, missing semicolons (no logic change) |
| `refactor` | Code restructure without feature or fix |
| `test` | Adding or updating tests |
| `chore` | Build process, config, dependencies |

### Examples:

```bash
git commit -m "feat(auth): add Google OAuth login"
git commit -m "fix(navbar): resolve dropdown overlap on mobile"
git commit -m "docs: add setup instructions to README"
git commit -m "chore: upgrade eslint to v9"
```

> ❌ Bad: `git commit -m "stuff"`, `git commit -m "fix"`, `git commit -m "AAAAAA"`
> ✅ Good: `git commit -m "fix(form): prevent empty submission on contact page"`

---

## 🚀 How to Push from a Branch

After committing your changes, push your branch to GitHub.

```bash
# First push (sets upstream tracking)
git push -u origin your-branch-name

# All subsequent pushes on the same branch
git push
```

### Full typical workflow:

```bash
# 1. Check which files changed
git status

# 2. Stage the files you want to commit
git add filename.js
# Or stage everything:
git add .

# 3. Commit with a descriptive message
git commit -m "feat(profile): add avatar upload functionality"

# 4. Push to GitHub
git push -u origin feat/profile-avatar-upload
```

After pushing, GitHub will often show a prompt at the top of your repo:
> *"feat/profile-avatar-upload had recent pushes — Compare & pull request"*

Click it to open a PR!

---

## 🔀 How to Create Pull Requests (PRs)

A Pull Request (PR) is a formal proposal to merge your branch into the main branch. It's where code review happens.

### Steps:

1. Push your branch to GitHub (see above).
2. Go to the repository on GitHub.
3. Click **"Compare & pull request"** (appears after a recent push) — or go to **Pull requests → New pull request**.
4. Set:
   - **base branch** → `main` (where you want to merge INTO)
   - **compare branch** → your feature branch (what you're merging FROM)
5. Write a clear PR title and description:
   - **Title:** Follow the same convention as commits → `feat(auth): add Google OAuth login`
   - **Description:** Explain *what* you changed, *why*, and *how to test it*
6. Assign **Reviewers** (teammates who should review your code).
7. Link related **Issues** if applicable (e.g., `Closes #12`).
8. Click **Create Pull Request**.

### PR Description Template (use this!):

```markdown
## What does this PR do?
Brief description of the changes.

## Why?
Reason for the change (links to issue if applicable).

## How to test?
Steps to verify the feature/fix works.

## Screenshots (if UI changes)
```

> 💡 **Rule of thumb:** Never merge your own PR if working in a team. Always get at least one teammate to review it first.

---

## 📋 How Kanban Works (GitHub Projects)

Kanban is a visual workflow system. In GitHub Projects, you organize your work as **cards** on a board with columns.

### Setting up a Kanban board:

1. Go to your GitHub repository.
2. Click the **Projects** tab → **New project**.
3. Select **Board** template (this gives you the Kanban layout).
4. Name it (e.g., `Sprint 1` or `Team Project Board`).

### Standard Kanban columns:

| Column | Meaning |
|--------|---------|
| **Backlog** | All tasks that exist but aren't started yet |
| **To Do** | Tasks planned for the current sprint/week |
| **In Progress** | Tasks actively being worked on |
| **In Review** | Task is done, PR is open and waiting for review |
| **Done** | Merged and complete |

### Workflow:

1. Create **Issues** in GitHub for every task (e.g., `feat: build login page`).
2. Add those Issues to your Project board — they appear as cards.
3. Assign each card to a team member.
4. As work progresses, **drag cards** between columns.
5. When a PR is merged, move the card to **Done** (or automate this in Project settings).

### Card naming convention (matches commit types):

```
feat: implement user registration form
fix: resolve broken redirect after login
docs: write API endpoint documentation
chore: configure ESLint rules
test: add unit tests for cart module
```

> 💡 You can link a PR directly to an Issue. When the PR is merged, the Issue closes automatically if you write `Closes #ISSUE_NUMBER` in the PR description.

---

## 🔄 What to Do When Your Teammate Pushed to Main While You're on Your Branch

This is one of the most common situations in team development. Your branch is now **behind** `main`, and you need to bring those new changes into your branch.

### Option 1: Rebase (recommended for clean history)

```bash
# 1. Fetch the latest changes from GitHub
git fetch origin

# 2. Rebase your branch on top of the updated main
git rebase origin/main
```

Rebase replays your commits on top of the latest `main` — keeping history linear and clean.

### Option 2: Merge (simpler, creates a merge commit)

```bash
# 1. Fetch and pull the latest main
git checkout main
git pull origin main

# 2. Go back to your branch and merge main into it
git checkout your-branch-name
git merge main
```

### After either option, push your updated branch:

```bash
# If you rebased, you'll need to force push (only safe if no one else uses your branch)
git push --force-with-lease

# If you merged, a normal push works
git push
```

> ⚠️ **Never rebase a branch that multiple teammates are working on together.** Rebase rewrites history, which causes problems for others. Use merge in that case.

> 💡 **Best habit:** Before starting work each day, always run:
> ```bash
> git checkout main
> git pull origin main
> git checkout your-branch
> git rebase origin/main
> ```

---

## ⚔️ How to Resolve Conflicts

Conflicts happen when two people edit the same lines of the same file. Git doesn't know which version to keep — so it asks you.

### What a conflict looks like in a file:

```
<<<<<<< HEAD (your branch)
const greeting = "Hello, world!";
=======
const greeting = "Hi there!";
>>>>>>> main
```

- Everything between `<<<<<<< HEAD` and `=======` is **your version**.
- Everything between `=======` and `>>>>>>>` is **the incoming version** (from main or your teammate's branch).

### Steps to resolve:

1. Open the conflicted file in your editor.
2. Decide which version to keep — yours, theirs, or a combination.
3. **Delete all the conflict markers** (`<<<<<<<`, `=======`, `>>>>>>>`).
4. The final file should only contain the correct, clean code.
5. Stage the resolved file:

```bash
git add filename.js
```

6. Continue the rebase or commit the merge:

```bash
# If you were rebasing:
git rebase --continue

# If you were merging:
git commit -m "fix: resolve merge conflict in greeting module"
```

### If things go wrong and you want to start over:

```bash
# Abort a rebase
git rebase --abort

# Abort a merge
git merge --abort
```

> 💡 **VS Code** has a built-in conflict resolver with "Accept Current Change / Accept Incoming Change / Accept Both" buttons — much easier than editing manually!

---

## ✅ Simulated Tasks (Your Kanban Cards)

Below are the tasks for this project. Create these as **GitHub Issues** and add them to your Kanban board. Assign one or more to each team member.

---

### 📌 Backlog

| # | Card Title | Type | Description |
|---|-----------|------|-------------|
| 1 | `feat: fork the team repo and clone locally` | feat | Each student forks the class repo, adds the upstream remote, and clones it |
| 2 | `chore: add all team members as collaborators` | chore | Repo owner adds teammates via Settings → Collaborators |
| 3 | `feat: create your first feature branch` | feat | Each student creates a branch using the `feat/` naming convention |
| 4 | `docs: write a short personal bio in /bios folder` | docs | Each student creates a markdown file in `/bios/` with their name and a few sentences |
| 5 | `feat: push branch and open a pull request` | feat | After committing the bio, push and open a PR following the PR template |
| 6 | `fix: review and approve a teammate's PR` | fix | Review another student's PR, leave at least one comment, then approve and merge |
| 7 | `chore: set up GitHub Projects Kanban board` | chore | Create a Board-type project, add all columns (Backlog → Done), and populate with these issues |
| 8 | `feat: simulate a merge conflict and resolve it` | feat | Two students edit the same file on different branches, then open PRs and resolve the conflict |
| 9 | `chore: sync your branch after a teammate merges to main` | chore | After a teammate's PR is merged, rebase your branch on top of the updated main |
| 10 | `docs: update README with what you learned` | docs | Add a "What I learned" section to the README in your own branch and open a PR |

---

### 📋 How to add these to GitHub Kanban:

1. Go to your repo → **Issues** → **New Issue** for each task above.
2. Title the issue exactly as written in the card title column.
3. In the description, paste the description and assign it to a team member.
4. Add the issue to your **Project board** — it will appear in **Backlog**.
5. Move it to **To Do** when you plan to start it, **In Progress** when you do, and **In Review** when your PR is open.

---

## 🧠 Quick Reference Cheat Sheet

```bash
# Clone a repo
git clone <url>

# Check status
git status

# Create & switch to branch
git checkout -b feat/my-feature

# Stage changes
git add .

# Commit
git commit -m "feat(scope): description"

# Push branch
git push -u origin feat/my-feature

# Sync with main (rebase)
git fetch origin
git rebase origin/main

# Abort if something goes wrong
git rebase --abort

# View all branches
git branch -a
```

---

> Made with 💙 for students learning Git collaboration. Remember: the best way to learn Git is to break things and fix them. That's what `git reflog` is for.
