---
layout: default
title: Troubelshooting
nav_order: 7
---

# Troubleshooting

### Installation Issues

#### Windows WSL2

**"WSL2 won't install — error about virtualization"**
Your computer's CPU virtualization feature is disabled. Restart your computer and enter the BIOS/UEFI settings (usually by pressing F2, F10, Del, or Esc during startup — your computer's manual will specify which). Look for a setting called "Intel Virtualization Technology", "Intel VT-x", "AMD-V", or "SVM Mode" and enable it. Save and restart.

**"conda not found after install"**
Close the Ubuntu terminal completely and reopen it. Conda modifies your shell configuration, and the change only takes effect in a new terminal session. If it still fails, run `source ~/.bashrc` and try again.

**"Permission denied when running run.sh"**
Run this once to make the script executable:

```bash
chmod +x /mnt/d/GNPS_Local/local_runner/run.sh
```

**"The server starts but I can't reach http://localhost:8000"**
Confirm that the Ubuntu terminal shows the `Uvicorn running` line. If it does and the browser still fails, try `http://127.0.0.1:8000` instead.

**Unable to create symlink, files too long**

1) Clone without checkout out files
```bash
git clone --no-checkout <your-repo-url>
cd <repo-name>
```

2) Disable symlinks in the local config
```bash
git config core.symlinks false
```

3) Force the checkout
```bash
git checkout
```

#### macOS

**"conda: command not found"**
Conda wasn't added to your PATH. Run:

```bash
source ~/.zprofile
```

Then try again. If that doesn't work, reinstall Miniconda:

```bash
brew reinstall miniconda
conda init zsh
source ~/.zprofile
```

**"gnps environment not found"**
Make sure you created the environment:

```bash
conda create -n gnps python=3.9
conda activate gnps
pip install -r requirements.txt
```

**"ModuleNotFoundError: No module named 'fastapi'"**
Make sure the `gnps` environment is activated:

```bash
conda activate gnps
```

If it's activated and still fails, reinstall packages:

```bash
pip install -r requirements.txt
```

**"Apple Silicon: Installation hangs or fails"**
Try specifying architecture flags:

```bash
conda activate gnps
ARCHFLAGS=-Qunused-arguments CPPFLAGS=-Qunused-arguments pip install -r requirements.txt
```

---

### Runtime Issues

**"Job is stuck on Queued and never starts"**
The server processes jobs in background threads. If the server was stopped and restarted, previously queued jobs will not automatically resume. Use the "Restart" button on the job page, or resubmit.

**"Step FAILED — how do I read the log?"**

The run log output is shown in the UI of every job:
```
http://localhost:8000/job/{job_id}
```

The run log is also saved to disk at:

**Windows WSL2:**
```bash
cat ~/gnps_jobs/JOBID/run.log | tail -100
```

**macOS:**
```bash
cat ~/gnps_jobs/JOBID/run.log | tail -100
```

The relevant error will be near the bottom, under a `STEP FAILED` line.

**"The server won't start — port 8000 is already in use"**
Another process (possibly a previous server instance) is using port 8000. Find and stop it:

**Windows WSL2 (Ubuntu):**
```bash
lsof -i :8000
kill -9 <PID shown above>
```

**macOS:**
```bash
lsof -i :8000
kill -9 <PID shown above>
```

Then restart the server.

**Alternatively, use a different port:**

**Windows WSL2:**
```bash
cd /mnt/d/GNPS_Local/local_runner
bash run.sh --port 8001
```

**macOS:**
```bash
cd ~/GNPS_Local/local_runner
python -m uvicorn app:app --host 127.0.0.1 --port 8001
```

Then open `http://localhost:8001` in your browser.

**"Upload fails or the form seems to hang"**
Large MGF files (>500 MB) may take a moment to upload over the localhost connection. Wait 30 seconds before assuming it has failed. The browser's network tab can confirm whether the upload is still in progress.

**"Reformat quantification FAILED — must input exactly 1 spectrum mgf file"**
Your input folder contains more than one file in the spectra folder. Only one MGF file is supported per job. Make sure you are uploading a single merged MGF (not one per sample).

**"My network looks wrong — very dense or all features connected"**
The cosine threshold may be too low. Resubmit with a higher "Cosine Score Threshold" (try 0.7 if you used a lower value). Also check that your MGF scan numbers match the `row ID` column in your feature table exactly.

---

### Getting Help

When reporting a problem, please include:

1. The **Job ID** (shown on the job page, e.g., `a3f9c12b`)
2. The last 50 lines of `~/gnps_jobs/{job_id}/run.log`
3. The name and source of your feature-finding software
4. Approximate number of features and samples
5. Your platform (Windows WSL2 or macOS Intel/Apple Silicon)

**To restart a failed job from scratch** (same files, same parameters):
Use the **Restart** button on the job page. This clears the output and log and re-runs the full pipeline.

**To delete a job entirely:**

**Windows WSL2:**
Locate the following in Windows File Explorer:
```
\\wsl.localhost\Ubuntu\home\{username}\gnps_jobs
```

Delete the entire job ID folder to delete a job. You can also use the Ubuntu terminal:

```bash
rm -rf ~/gnps_jobs/JOBID
```

**macOS:**
In Terminal, delete the job:

```bash
rm -rf ~/gnps_jobs/JOBID
```
