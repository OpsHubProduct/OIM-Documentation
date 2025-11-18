# Contribution Guide for New GitHub Users

This guide explains **step by step** how to contribute to the documentation, even if you are completely new to Git and GitHub.  
It also includes important notes because the repository is **public**.

Repository URL:  
🔗 **https://github.com/OpsHubProduct/OIM-Documentation.git**

---

# ⚠️ Important: Public Repository Notice

This repository is **public**, which means:

- Anyone on the internet can **view and download** the repository.
- Only approved contributors from the OpsHubProduct organization can **push changes** or create branches.
- External users may fork the repository and submit **Pull Requests (PRs)**.
- **Do NOT upload sensitive, confidential, or internal information**, including:
  - credentials (passwords, API keys, tokens)
  - customer-specific data
  - server URLs or internal IPs
  - proprietary code or scripts

Always verify the content before committing.

---

# Before You Start

## Install Git
- Download Git (search “Git download”).
- Install with default settings.
- Check installation:

```bash
git --version
```

---

## Set Up or Log Into GitHub

1. Go to GitHub in your browser.
2. Create an account or sign in.
3. Make sure you have been granted contributor access to OpsHubProduct.

---

# Clone the Repository (First-Time Setup)

Cloning downloads the repository to your computer.

1. Open **Git Bash**, **Terminal**, or **Command Prompt**.
2. Go to the folder where you want to keep the project:

```bash
cd path/to/your/folder
```

3. Clone the repository:

```bash
git clone https://github.com/OpsHubProduct/OIM-Documentation.git
```

4. Navigate into the project folder:

```bash
cd OIM-Documentation
```

You only need to do this **once**.

---

# Understanding Branches (Beginner Friendly)

Branches allow multiple people to work without interfering.

- `DevSpace` → main working branch
- Always create your own new branch **from `DevSpace`**
- Never make changes directly on:
  - `main`
  - other branches(except the new branch created by the user)

---

# Switch to DevSpace and Pull Latest Updates

```bash
git checkout DevSpace
git pull
```

Ensures your local files are up-to-date.

---

# Create Your Own Working Branch

Choose a descriptive name:

```bash
git checkout -b your-branch-name
```

Examples:

```bash
git checkout -b doc-update-markdown-basics
git checkout -b fix-typo-setup-guide
```

---

# Make Changes to Documentation

- Open the folder in VS Code / IntelliJ / any editor.
- Edit `.md` files as needed.
- Save your changes.
> For Markdown, formatting related guide, refer to the [format guide](./gitbook-markdown-basics.md).

---

# Review Your Changes

See which files changed:

```bash
git status
```

See details:

```bash
git diff
```

---

# Stage and Commit Your Changes

### Stage everything:

```bash
git add .
```

### Commit with a clear message:

```bash
git commit -m "Updated markdown basics documentation"
```

There is **no strict commit format**, but clarity is important.

---

# Push Your Branch to GitHub

```bash
git push origin your-branch-name
```

Your branch will now appear on GitHub.

---

# Create a Pull Request (PR)

1. Visit the repo in your browser.
2. GitHub may show a banner: **“Compare & Pull request”**.
3. Or go manually:
   - Pull Requests → New Pull Request 
   - Base branch → `DevSpace`
   - Compare branch → *your branch*
4. Fill:
   - PR title 
   - PR description (what & why)
5. Set **approver** → `OpsHubProduct`
6. Click **Create Pull Request**

---

# PR Review & Approval

- Product Team reviews the PR.
- They may leave comments.
- To address changes:

```bash
git add .
git commit -m "Addressed review comments"
git push
```

Your PR updates automatically.

After approval, the PR is merged.

---

# Keep Your Local Copy Updated

Before starting new work:

```bash
git checkout DevSpace
git pull
git checkout -b new-branch
```

Never reuse old branches for new tasks.

---

# Quick Summary (Cheat Sheet)

```bash
git clone https://github.com/OpsHubProduct/OIM-Documentation.git
cd OIM-Documentation

git checkout DevSpace
git pull
git checkout -b my-branch

git add .
git commit -m "Meaningful message"
git push origin my-branch
```

---

You are now ready to contribute safely and confidently to a **public repository**! 🎉  
