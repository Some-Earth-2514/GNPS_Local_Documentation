---
layout: default
title: Quick Start
nav_order: 5
---

# Quick Start

## Upload Spectral Libraries

Libraries are `.mgf` files used for **library search** steps in FBMN and Molecular Networking workflows.
1. Click the **Settings gear icon** in the top-right corner.
2. Navigate to **Manage Libraries**.
3. Upload your libraries, open source ones can be found [here](https://external.gnps2.org/gnpslibrary).

## Prepare Your Data

For Feature-Based Molecular Networking (FBMN), you need three things:

| File | What it is | Where it comes from |
|---|---|---|
| **MS/MS spectra** (.mgf) | Your raw fragmentation spectra, exported from MZmine/XCMS/MS-DIAL | Your feature-finding software |
| **Feature quantification table** (.csv) | A table of detected features with m/z, RT, and intensity per sample | Your feature-finding software |
| **Metadata table** (.tsv) optional | Sample group assignments <br> (e.g., treatment vs. control) | You create this |

**File format requirements at a glance:**

- The MGF file must have `SCANS=` or `FEATURE_ID=` fields that match the row IDs in your feature table.
- The feature table must have columns named `row ID`, `row m/z`, `row retention time`, plus one `[filename] Peak area` column per sample.
- Metadata must have a `filename` column whose values exactly match the sample file names in your feature table.

See [Data Format](https://some-earth-2514.github.io/GNPS_Local_Documentation/docs/data-format.html) for detailed column requirements and examples.

---

## Submit a Job

1. Open **http://localhost:8000** in your browser.
2. Click **"Feature-Based Molecular Networking"**.
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

## Monitor Progress

The job page shows:

- **Status badge** updates automatically — (Queued → Running → Done/Failed/Cancelled)
- **Parameters** — to track job specifications
- **Output Files** — appear here as each step completes
- **Step Timing** — a visual tool to track how long each step takes
- **Run Log** — a live stream of every step the pipeline is executing

If a step fails, the log will show `STEP FAILED (exit 1)` with an error message. See [Troubleshooting](https://some-earth-2514.github.io/GNPS_Local_Documentation/docs/troubleshooting.html) for common causes.

---

## Download and View Results

When the job shows **Done**, the Output Files panel lists all results. Key files:

| File | What it contains |
|---|---|
| `gnps_molecular_network.graphml` | The molecular network — open this in Cytoscape |
| `clusterinfo_summary_enriched.tsv` | One row per feature: m/z, RT, intensity, library match, component |
| `librarysearch_results_db.tsv` | All library hits with compound names, scores, SMILES |
| `components_table.tsv` | One row per connected network component |
| `networking_pairs_filtered.tsv` | All edges: which features are similar and by how much |

**To visualize the network:**

1. Download and install [Cytoscape](https://cytoscape.org) (free, cross-platform).
2. In Cytoscape: **File → Import → Network from File**, select your `.graphml` file.
3. Each node is a detected feature. Node color can be mapped to compound annotation; edge width to cosine score.
