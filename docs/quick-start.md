---
layout: default
title: Quick Start
nav_order: 5
---

# Quick Start

## 5. Quick Start: Your First Analysis

### 5a. Prepare Your Data

For Feature-Based Molecular Networking (FBMN), you need three things:

| File | What it is | Where it comes from |
|---|---|---|
| **MS/MS spectra (.mgf)** | Your raw fragmentation spectra, exported from MZmine/XCMS/MS-DIAL | Your feature-finding software |
| **Feature quantification table (.csv)** | A table of detected features with m/z, RT, and intensity per sample | Your feature-finding software |
| **Metadata table (.tsv) — optional** | Sample group assignments (e.g., treatment vs. control) | You create this |

**File format requirements at a glance:**

- The MGF file must have `SCANS=` or `FEATURE_ID=` fields that match the row IDs in your feature table.
- The feature table must have columns named `row ID`, `row m/z`, `row retention time`, plus one `[filename] Peak area` column per sample.
- Metadata must have a `filename` column whose values exactly match the sample file names in your feature table.

See [Section 9](#9-data-format-reference) for detailed column requirements and examples.

---

### 5b. Submit a Job

1. Open **http://localhost:8000** in your browser.
2. Click **"Feature-Based Molecular Networking"** (the primary, recommended workflow).
3. On the submission form:
   - **Input Spectra (MGF):** Click the upload box and select your `.mgf` file.
   - **Quantification Table:** Upload your feature table (`.csv`).
   - **Feature Table Source:** Select the software you used (e.g., MZmine2, MZmine3, MS-DIAL).
   - **Metadata Table (optional):** Upload if you have sample grouping information.
4. The networking and library search parameters are pre-filled with sensible defaults — you do not need to change them for your first run.
5. Optionally fill in a **Job Name** (e.g., "My_Experiment_Pos_Mode") to help identify the job later.
6. Click **"Submit Job"**.

You will be redirected to a job status page automatically.

---

### 5c. Monitor Progress

The job page shows:

- **Status badge** (Queued → Running → Done/Failed) — updates automatically
- **Run Log** — a live stream of every step the pipeline is executing
- **Output Files** — appear here as each step completes

Typical runtimes depend on data size:

| Dataset size | Approximate time |
|---|---|
| <500 features, 1 library | 2–5 minutes |
| 1,000–3,000 features, 1 library | 5–20 minutes |
| >5,000 features | 30+ minutes |

If a step fails, the log will show `STEP FAILED (exit 1)` with an error message. See [Troubleshooting](#runtime-issues) for common causes.

---

### 5d. Download and View Results

When the job shows **Done**, the Output Files panel lists all results. Key files:

| File | What it contains |
|---|---|
| `gnps_molecular_network.graphml` | The molecular network — open this in Cytoscape |
| `clusterinfo_summary_enriched.tsv` | One row per feature: m/z, RT, intensity, library match, component |
| `librarysearch_results_db.tsv` | All library hits with compound names, scores, SMILES |
| `components_table.tsv` | One row per connected network component |
| `networking_pairs_filtered.tsv` | All edges: which features are similar and by how much |

**To visualize the network:**

1. Download and install **Cytoscape** from [https://cytoscape.org](https://cytoscape.org) (free, cross-platform).
2. In Cytoscape: **File → Import → Network from File**, select your `.graphml` file.
3. Each node is a detected feature. Node color can be mapped to compound annotation; edge width to cosine score.
