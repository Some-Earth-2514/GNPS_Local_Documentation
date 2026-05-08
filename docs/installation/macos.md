---
layout: default
title: MacOS Setup
parent: Installation
nav_order: 2
---

# macOS SETUP

### 4a. Check Your Mac Chip

Open **Terminal** (Applications → Utilities → Terminal) and run:

```bash
uname -m
```

**Output meanings:**
- `x86_64` = Intel Mac
- `arm64` = Apple Silicon Mac (M1/M2/M3/etc.)

Note your result — you'll need it below.

---

### 4b. Install Homebrew (macOS)

Homebrew is a package manager for macOS. Install it first:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

If you're on **Apple Silicon (M1/M2/M3)**, add Homebrew to your PATH:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verify it works:

```bash
brew --version
```

---

### 4c. Install Git (macOS)

```bash
brew install git
```

Verify:

```bash
git --version
```

---

### 4d. Install Conda (macOS)

We recommend **Miniconda** (lightweight) or **Anaconda** (full-featured). For most users, Miniconda is sufficient.

#### Option A: Miniconda (recommended)

```bash
brew install miniconda
conda init zsh
```

Then close and reopen Terminal, or run:

```bash
source ~/.zprofile
```

#### Option B: Anaconda

```bash
brew install anaconda
conda init zsh
source ~/.zprofile
```

Verify conda works:

```bash
conda --version
```
