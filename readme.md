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
