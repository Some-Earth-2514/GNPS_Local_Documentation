---
layout: default
title: Windows WSL2 Setup
parent: For Developers
nav_order: 1
---

# Windows WSL2 Setup
### 4a. Enable WSL2 on Windows 11

**What is WSL2?** Think of it as a lightweight Linux computer running invisibly inside Windows. GNPS Local's analysis tools are Linux programs, so they need this Linux layer to run. You do not need to understand Linux to use it — you just need it running in the background.

**Step 1:** Open the Start menu, search for **PowerShell**, right-click it, and select **"Run as administrator"**.

**Step 2:** Copy and paste this command, then press Enter:

```powershell
wsl --install
```

**What you should see:**

```
Installing: Virtual Machine Platform
Virtual Machine Platform has been installed.
Installing: Windows Subsystem for Linux
Windows Subsystem for Linux has been installed.
Installing: Ubuntu
Ubuntu has been installed.
The requested operation is successful.
```

**Step 3:** **Restart your computer** when prompted. This is required.

> **If you see an error like "WSL 2 requires an update to its kernel component"**, run this additional command after the restart:
> ```powershell
> wsl --update
> ```

> **If you see "Virtualization is not enabled"**, your computer's BIOS needs a small change — see [Troubleshooting](#installation-issues).

---

### 4b. Install Ubuntu 24.04

After your restart, Ubuntu may open automatically and ask you to set up a username and password. If it does not open automatically:

1. Open the **Start menu** and search for **Ubuntu**.
2. Click **Ubuntu** (or **Ubuntu 24.04**) to open the Linux terminal.

**Set up your Linux username and password:**

```
Enter new UNIX username: yourusername
New password: (type a password — it won't show as you type, that's normal)
Retype new password:
passwd: password updated successfully
```

> **Remember this password** — you will need it occasionally for system commands.

**Verify WSL2 is running correctly.** In PowerShell (not Ubuntu), run:

```powershell
wsl --list --verbose
```

You should see output like:

```
  NAME            STATE           VERSION
* Ubuntu-24.04    Running         2
```

The `VERSION 2` confirms WSL2 is active. You are ready to proceed.

---

### 4c. Install System Dependencies (Windows WSL2)

Before setting up your Python environment, you must ensure your Ubuntu system has the basic tools needed to run C++ analysis modules.

In your Ubuntu terminal, copy and paste this single line:

```bash
sudo apt update && sudo apt install -y build-essential libgomp1
```

**Why is this needed?** `build-essential` installs the C++ compiler (g++) and `libgomp1` provides the library for parallel processing. GNPS Local uses these to run high-performance calculations on your data. You will be asked for your Linux password to run this.

---

### 4d. Install Conda (Miniconda) — Windows WSL2

Conda is a tool that manages Python packages — think of it as an app store for scientific Python software that keeps everything neatly organized so different tools don't conflict with each other.

Open your **Ubuntu terminal** and run these commands one at a time:

**Download the installer:**

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
```

**Run the installer:**

```bash
bash ~/miniconda.sh
```

- Press **Enter** to scroll through the license agreement.
- Type `yes` to accept the license.
- Press **Enter** to accept the default install location (`/home/yourusername/miniconda3`).
- Type `yes` when asked to initialize conda.

**Apply the changes:**

```bash
source ~/.bashrc
```

**Verify it worked:**

```bash
conda --version
```

You should see something like `conda 24.x.x`. If you see "command not found", close and reopen the Ubuntu terminal and try again.
