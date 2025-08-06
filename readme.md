# 📘 Git Tutorial Practice – By Manali

This README summarizes the basic Git commands I used while learning version control and pushing my project to GitHub.

## 🛠 Project Setup

```bash
git init
```

Initializes a new local Git repository.

## 🌿 Branch Management

```bash
git branch
```

Lists existing branches (by default, it's usually `master` or `main`).

## 📥 Staging & Committing

```bash
git add .\authentication.txt
```

Stages the specified file for commit.

```bash
git commit -m "sign up completed"
```

Commits the staged changes with a meaningful message.

## 👤 Git Configuration

```bash
git config --global user.email "manalisambhavani2015@gmail.com"
git config --global user.name "Manali"
git config --list
git config --list --global
```

Sets up user identity and verifies Git configuration settings.

## 📊 Repository Status & Logs

```bash
git status
```

Displays the state of the working directory and staging area.

```bash
git log
```

Shows the commit history.

## 🌍 Remote Repository Setup

```bash
git remote add origin https://github.com/manalisambhavani/git-tutorial.git
git remote -v
```

Connects the local repository to a GitHub repository and verifies it.

## 🚀 Push to GitHub

```bash
git push --set-upstream origin master
git push
```

Pushes changes to the remote repository and sets the upstream branch.

---

Absolutely! Here's a clear breakdown of what a **branch in Git** is and why it's so useful:

---

### 🌿 What Is a Git Branch?

A **branch** in Git is like a separate workspace or timeline for your code. It allows you to work on new features, bug fixes, or experiments **without affecting the main codebase** (usually called `main` or `master`).

Think of it as a “parallel universe” for your project:

-   You can make changes freely.
-   When you're happy with the results, you **merge** the branch back into the main project.
-   If things go wrong, you can discard the branch without harming the main code.

---

### 🛠️ Why Use Branches?

Branches are essential for:

-   **Developing new features** without disrupting the live code.
-   **Fixing bugs** while keeping the main branch stable.
-   **Experimenting** with ideas safely.
-   **Collaborating** with others—each person can work on their own branch.

---

### 📌 Common Git Branch Commands

| Action             | Command                       | Description                               |
| ------------------ | ----------------------------- | ----------------------------------------- |
| Create a branch    | `git branch new-feature`      | Makes a new branch called `new-feature`   |
| Switch to a branch | `git checkout new-feature`    | Moves you to the `new-feature` branch     |
| Create and switch  | `git checkout -b new-feature` | Shortcut to create and switch in one step |
| List branches      | `git branch`                  | Shows all branches in your repo           |
| Delete a branch    | `git branch -d new-feature`   | Deletes the branch (after merging)        |

---

### 🔄 Real-Life Example

Let’s say you’re building a resin art showcase web app (😉):

1. You’re on the `main` branch.
2. You want to add a gallery feature → create a branch `gallery-feature`.
3. You build and test the gallery in that branch.
4. Once it’s ready, you merge `gallery-feature` into `main`.

This way, your main app stays stable while you experiment and build in isolation.

---

Would you like to try creating a branch in a sample project together? Or explore how merging works next?
