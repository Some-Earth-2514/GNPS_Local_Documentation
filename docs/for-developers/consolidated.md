---
layout: default
title: Consolidated Setup
parent: For Developers
nav_order: 3
---

# Consolidated Setup Steps
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
