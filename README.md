# 🧑‍💻 GitHub Collaboration Guide

This is your complete reference for working with Git and GitHub as a team.
Read it top to bottom once, then use it as a reference while you work.

The actual tasks you need to complete are in `TASKS.md`.

---

## 📚 Start Here — Recommended Resources

Go through at least one of these before you begin:

1. [**GitHub Skills**](https://skills.github.com/) — Hands-on exercises directly inside GitHub. Best starting point.
2. [**Atlassian Git Tutorials**](https://www.atlassian.com/git/tutorials) — Visual explanations of every Git concept.
3. [**Pro Git Book**](https://git-scm.com/book/en/v2) — The full official reference. Chapters 1–3 are enough.
4. [**Oh My Git!**](https://ohmygit.org/) — A game that teaches Git visually.

---

## 1. How to Fork the Repository

> Do this once at the start of the project.
> If you are added as a collaborator with write access, you can clone the shared repository directly instead of forking. If you do not have write access, fork the repository first and work from your fork.

1. Open the repository page on GitHub.
2. Click **Fork** in the top-right corner.
3. Select your personal account as the destination.
4. Open your terminal.
5. Run `git clone https://github.com/YOUR_USERNAME/REPO_NAME.git`
6. Run `cd REPO_NAME`
7. Run `git remote add upstream https://github.com/ORIGINAL_OWNER/REPO_NAME.git`
8. Run `git remote -v` — confirm you see both `origin` and `upstream`.

> `origin` points to your fork. `upstream` points to the original repo.

---

## 2. How to Add Collaborators

> Only the repository owner does this.

1. Go to the repository on GitHub.
2. Click **Settings**.
3. Click **Collaborators** in the left sidebar.
4. Click **Add people**.
5. Search for your teammate's GitHub username.
6. Click **Add [username] to this repository**.
7. Repeat steps 4–6 for every teammate.
8. Ask teammates to check their email and accept the invitation.

---

## 3. How to Set Up the Kanban Board

1. Go to the repository on GitHub.
2. Click the **Projects** tab.
3. Click **New project**.
4. Select the **Board** template.
5. Name it `Sprint 1`.
6. Click **Create project**.
7. Set the columns to: `Backlog` → `To Do` → `In Progress` → `In Review` → `Done`.
8. Go to `TASKS.md` and create a GitHub Issue for each task.
9. Open the board and add each issue as a card under **Backlog**.
10. Assign each card to a team member.

### How the board moves

- When a task is not started yet → keep it in **Backlog**
- When you plan to work on the task next → move it to **To Do**
- When you create a branch and start editing files → move it to **In Progress**
- When your PR is open → move it to **In Review**
- When the PR is approved and merged → move it to **Done**

---

## 4. How to Create and Name a Branch

> Do this every time you start a new task.

1. Run `git checkout main`
2. Run `git pull origin main`
3. If you are working from a fork, make sure your fork is synced with the original repository before creating a branch.
4. Run `git checkout -b type/short-description`

### Branch naming pattern

```
type/short-description
```

| Type | When to use |
|------|-------------|
| `feat` | Adding something new |
| `fix` | Fixing a bug or mistake |
| `docs` | Documentation only |
| `refactor` | Restructuring without changing content |
| `chore` | Config, structure, tooling |

**Good examples:**
```
feat/add-deployment-guide
fix/broken-links-in-intro
docs/improve-commit-section
chore/reorganize-folder-structure
```

---

## 5. How to Name Commits

### Commit message pattern

```
type(scope): short description
```

- `type` — same types as branch naming
- `scope` — the file or section affected, e.g. `readme`, `tasks`, `intro`
- `short description` — lowercase, present tense, no period at the end

**Good examples:**
```
feat(readme): add branching section with examples
fix(tasks): correct broken link in task 3
docs(intro): rewrite opening paragraph for clarity
chore: move images into /assets folder
```

### Making a commit

1. Run `git status`
2. Run `git add .` to stage everything, or `git add filename.md` for a specific file
3. Run `git commit -m "type(scope): your description"`

---

## 6. How to Push Your Branch

1. Run `git push -u origin your-branch-name` on your first push from this branch.
2. Run `git push` for every push after that.

---

## 7. How to Create a Pull Request

1. Go to the repository on GitHub after pushing.
2. Click **Compare & pull request**.
3. Set **base** to `main` and confirm **compare** is your branch.
4. Write the PR title using the same convention as commits: `feat(readme): add branching section`
5. Fill in the description:

```
## What does this PR do?

## Why?

## How to review it?
```

6. Assign at least one teammate as **Reviewer**.
7. Write `Closes #ISSUE_NUMBER` in the description to link the Issue. If the Issue is in another repository, use the full format: `Closes OWNER/REPO#ISSUE_NUMBER`.
8. Click **Create Pull Request**.
9. Move your Kanban card to **In Review**.

> Do not merge your own PR. Wait for your reviewer to approve it.

---

## 8. What to Do When a Teammate Merges to Main

> Run this every time before you start working, and whenever you see a new merge on `main`.

1. Run `git fetch origin`
2. Run `git checkout your-branch-name`
3. Run `git rebase origin/main`
4. If there are no conflicts, run `git push --force-with-lease`
5. If there are conflicts, continue to the next section.

---

## 9. How to Resolve Conflicts

When two people edited the same part of the same file, Git will pause and show you this inside the file:

```
<<<<<<< HEAD
your version of the line
=======
your teammate's version of the line
>>>>>>> origin/main
```

1. Open the conflicted file in your editor.
2. Find all the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
3. Decide which version to keep — yours, theirs, or a mix of both.
4. Delete the three marker lines entirely.
5. Save the file.
6. Run `git add filename.md`
7. Run `git rebase --continue`
8. If Git shows another conflict, repeat steps 1–7 until the rebase finishes.
9. Run `git push --force-with-lease`

> If something goes wrong at any point, run `git rebase --abort` to undo the rebase and go back to where you started.

---

## Quick Reference

```bash
# Start a new task
git checkout main
git pull origin main
git checkout -b feat/your-task

# Save your work
git status
git add .
git commit -m "feat(scope): description"

# Push
git push -u origin feat/your-task

# Sync with main
git fetch origin
git rebase origin/main

# Something went wrong
git rebase --abort
```
