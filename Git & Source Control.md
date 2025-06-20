## Git & Source Control

* What is Git?
* Basic Git Workflow
* Common Git Commands
* Branching Strategy
    * `main` branch
    * `develop` branch
    * `feature` branches
    * `task` branches
* Working with Remotes
* Best Practices

---

## 1. What is Git?

Git is a distributed version control system used to track changes in source code. It allows collaboration, branching, and reverting changes efficiently.

---

## 2. Basic Git Workflow

```bash
# Clone the repository
git clone https://github.com/your-org/your-repo.git

# Create or switch to a new branch
git checkout -b feature/login-screen

# Stage changes
git add .

# Commit changes
git commit -m "Add login screen UI"

# Push to remote
git push origin feature/login-screen

# Create a Pull Request (PR) on GitHub
```

---

## 3. Common Git Commands

| Command                            | Purpose                              |
|------------------------------------|--------------------------------------|
| `git status`                       | Show working directory state         |
| `git add <file>`                   | Stage changes                        |
| `git commit -m "message"`          | Commit staged changes                |
| `git push`                         | Push to remote repository            |
| `git pull`                         | Pull latest changes from remote      |
| `git checkout -b <branch>`         | Create and switch to new branch      |
| `git merge <branch>`              | Merge another branch into current    |
| `git log`                          | Show commit history                  |
| `git stash`                        | Temporarily save uncommitted changes|

---

## 4. Branching Strategy

Following a branching strategy helps maintain clean and collaborative development.

### 4.1 `main` Branch

- Contains production-ready code.
- All releases are merged into `main`.
- Protected from direct pushes.

### 4.2 `develop` Branch

- Active development happens here.
- All feature and task branches are merged into `develop`.

```bash
git checkout develop
git pull origin develop
```

### 4.3 `feature` Branches

- New features should have their own branch.
- Naming: `feature/<feature-name>`

```bash
git checkout -b feature/payment-integration
```

- Merge into: `develop`

### 4.4 `task` Branches

- Use for sub-tasks or bug fixes.
- Naming: `task/<task-id>-<brief-description>`

```bash
git checkout -b task/123-fix-login-button
```

- Merge into: related `feature/` or `develop` branch.

---

## 5. Working with Remotes

```bash
# View remotes
git remote -v

# Add a new remote
git remote add origin https://github.com/user/repo.git

# Push a new branch
git push -u origin feature/my-feature

# Fetch all branches
git fetch --all
```

---

## 6. Best Practices

- Always **pull before pushing** to avoid conflicts.
- Use **clear and descriptive commit messages**.
- Keep branches small and focused.
- **Rebase** for clean history, but never rebase shared branches.
- Use **Pull Requests** (PRs) for peer reviews and CI/CD triggers.
