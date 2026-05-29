---
layout: default
title: Installation
nav_order: 3
---

# Installation
## 1. Download GNPS Local

You have two options:

- [ ] **GitHub Desktop**
- [ ] **ZIP download**

### GitHub Desktop (Recommended)
GitHub Desktop is a simple graphical tool that keeps your local code synchronized with the latest version. When updates are released, you can fetch them with one click instead of re-downloading everything.

**1:** Download and install [GitHub Desktop](https://desktop.github.com). Sign in with your GitHub account.

**2:** Visit the [GNPS Local repository](https://github.com/Some-Earth-2514/GNPS_Local) on GitHub and click **Fork** in the top-right corner. This creates a personal copy under your account that you can sync when updates are released.

**3:** In GitHub Desktop, go to **File → Clone Repository**, select your fork of `GNPS_Local`, and choose where to save it.

- **Windows:** Choose `D:\GNPS_Local` (or another Windows path)
- **macOS:** Choose `~/GNPS_Local` (your home directory)

GitHub Desktop will download all the code automatically.<br>
Visit [Troubleshooting](https://some-earth-2514.github.io/GNPS_Local_Documentation/docs/troubleshooting.html) if it throws an error "**Unable to create symlink, files too long**".

**4:** Whenever a new version is released, GitHub Desktop will notify you. Click **Fetch origin** and then **Pull** to download the updates.

### ZIP Download

If you don't have a GitHub account or prefer not to use GitHub Desktop, download the code as a ZIP file instead.

**1:** Visit the [GNPS Local repository](https://github.com/Some-Earth-2514/GNPS_Local) and click the green **Code** button, then select **Download ZIP**.

**2:** Unzip the downloaded file.

- **Windows:** Place the folder in a convenient location on Windows, such as `D:\GNPS_Local`
- **macOS:** Place the folder in your home directory, such as `~/GNPS_Local`

**To receive updates later:** You will need to manually download and unzip a new version from GitHub when releases are announced. This is more cumbersome than GitHub Desktop, but it works fine if you prefer to avoid GitHub altogether.

---
## 2. Start GNPS Local
 
- **Windows/macOS**: Open **Docker Desktop** from your Applications folder or system tray
- **Linux**: Check with `docker --version`
If you see a version number, Docker is ready.
 
### Build using Docker
 
```bash
# navigate to project root
cd D:\GNPS_Local

# ensure Docker is running and build the project
docker compose up --build
```
 
**Output** (First runtime 5–10 minutes):
```
#19 DONE 0.0s
[+] up 2/2
 ✔ Image gnps-local:latest     Built       189.3s
 ✔ Container gnps-local        Recreated   2.7s
Attaching to gnps-local
gnps-local  | INFO:     Started server process [7]
gnps-local  | INFO:     Waiting for application startup.
gnps-local  | INFO:     Application startup complete.
gnps-local  | INFO:     Uvicorn running on http://localhost:8000 (Press CTRL+C to quit)
gnps-local  | INFO:     127.0.0.1:39792 - "GET / HTTP/1.1" 200 OK
```

### Open in Browser

Navigate to **http://localhost:8000**

You should see the GNPS Local home page with workflow options.

---
## 3. Normal startup

Running GNPS Local after installation is immediate using your choice of commands below.

```bash
# Foreground - you can see logs
docker compose up

# Background - frees up your terminal
docker compose up -d

# Check status
docker compose ps

# View logs
docker compose logs -f

# Stop everything
docker compose down
```