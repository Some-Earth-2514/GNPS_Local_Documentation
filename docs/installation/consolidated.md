---
layout: default
title: Consolidated Setup
parent: Installation
nav_order: 3
---

# Consolidated Setup Steps
### 4e. Get the GNPS Local Code

You have two options: **GitHub Desktop (recommended)** or **ZIP download**. GitHub Desktop makes it easy to download the code and receive updates when new versions are released — no command line required.

#### Option 1: GitHub Desktop (Recommended)

**Why use this?** GitHub Desktop is a simple graphical tool that keeps your local code synchronized with the latest version. When updates are released, you can fetch them with one click instead of re-downloading everything.

**Step 1:** Download and install **GitHub Desktop** from [https://desktop.github.com](https://desktop.github.com). Sign in with your GitHub account (create a free account if you don't have one).

**Step 2:** Visit the GNPS Local repository on GitHub and click **Fork** in the top-right corner. This creates a personal copy under your account — you now have your own version that you can sync.

**Step 3:** In GitHub Desktop, go to **File → Clone Repository**, select your fork of `GNPS_Local`, and choose where to save it.

- **Windows WSL2:** Choose `D:\GNPS_Local` (or another Windows path)
- **macOS:** Choose `~/GNPS_Local` (your home directory)

GitHub Desktop will download all the code automatically.

**Step 4:** Whenever a new version is released, GitHub Desktop will notify you. Click **Fetch origin** and then **Pull** to download the updates. Your local changes (if any) are preserved.

**Step 5: For use in your terminal:**

**Windows WSL2:**
In your Ubuntu terminal, navigate to the downloaded folder:

```bash
cd /mnt/d/GNPS_Local
```

> **Note:** `/mnt/d/` is how WSL2 sees your `D:\` drive. If your GNPS Local folder is on `C:\`, use `/mnt/c/` instead.

**macOS:**
In Terminal, navigate to the downloaded folder:

```bash
cd ~/GNPS_Local
```

---

#### Option 2: ZIP Download (If You Don't Have GitHub)

If you don't have a GitHub account or prefer not to use GitHub Desktop, download the code as a ZIP file instead.

**Step 1:** Visit the GNPS Local GitHub repository and click the green **Code** button, then select **Download ZIP**.

**Step 2:** Unzip the downloaded file.

- **Windows WSL2:** Place the folder in a convenient location on Windows, such as `D:\GNPS_Local`
- **macOS:** Place the folder in your home directory, such as `~/GNPS_Local`

**Step 3: Access from terminal:**

**Windows WSL2:**
In your Ubuntu terminal, navigate to that folder:

```bash
cd /mnt/d/GNPS_Local
```

> **Note:** If your folder is on `C:\` instead of `D:\`, use `/mnt/c/` in the Ubuntu path instead.

**macOS:**
In Terminal, navigate to that folder:

```bash
cd ~/GNPS_Local
```

**To receive updates later:** You will need to manually download and unzip a new version from GitHub when releases are announced. This is more cumbersome than GitHub Desktop, but it works fine if you prefer to avoid GitHub altogether.

---

### 4f. Create the Python Environment

This step downloads and installs all the Python packages GNPS Local needs. It may take **5–15 minutes** depending on your internet speed — this is the longest step, but you only do it once.

**Windows WSL2:** In your Ubuntu terminal, navigate to your project folder:

```bash
cd /mnt/d/GNPS_Local
conda env create -f environment_windows.yml
```

**macOS:** In Terminal, navigate to your project folder:

```bash
cd ~/GNPS_Local
conda env create -f environment_mac.yml
```

Activate the environment:

```bash
conda activate gnps
```

**macOS only:** If you see warnings about architecture mismatches during installation, they're usually safe to ignore. If installation fails, try:

```bash
ARCHFLAGS=-Qunused-arguments CPPFLAGS=-Qunused-arguments pip install -r requirements.txt
```

---

### 4g. Start the Server

Every time you want to use GNPS Local, start the server from your terminal. You leave this terminal window open while you work.

**Windows WSL2:**

First time only — fix line endings (Linux uses LF, but cloning on Windows may have created CRLF line endings):

```bash
cd /mnt/d/GNPS_Local/local_runner
sed -i 's/\r$//' run.sh
```

Then start the server:

```bash
conda activate gnps
bash run.sh
```

**Expected output:**

```
  GNPS Local
  ────────────────────────────────
  Open in browser: http://localhost:8000
  Jobs stored in:  ~/gnps_jobs/
  Repo at:         /mnt/d/GNPS_Local
  Stop with:       Ctrl+C

INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
```

Open your Windows browser (Chrome, Edge, Firefox) and go to **http://localhost:8000**.

---

**macOS:**

```bash
cd ~/GNPS_Local/local_runner
conda activate gnps
python -m uvicorn app:app --host 127.0.0.1 --port 8000
```

**Expected output:**

```
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
```

Open your browser and go to **http://localhost:8000**.

---

**Both platforms:** You should see the GNPS Local home page with three workflow cards.

> **To stop the server:** Press `Ctrl+C` in your terminal.

---

### 4h. Updates

You only need to update when new versions of GNPS Local are released.

**If you cloned with GitHub Desktop:**

Open GitHub Desktop, and it will notify you when updates are available. Click **Fetch origin** and then **Pull** to download the updates.

**If you cloned with Git (command line):**

**Windows WSL2:**

```bash
cd /mnt/d/GNPS_Local
git pull origin main
```

**macOS:**

```bash
cd ~/GNPS_Local
git pull origin main
```

**If you forked the repo:**

Click the **"Sync fork"** button on your GitHub fork, then use the git commands above.

**After updating:**

You may need to reinstall Python dependencies. Run these commands:

**Windows WSL2:**

```bash
cd /mnt/d/GNPS_Local/local_runner
conda activate gnps
pip install -r requirements.txt
```

**macOS:**

```bash
cd ~/GNPS_Local/local_runner
conda activate gnps
pip install -r requirements.txt
```
