---
layout: default
title: Advanced Usage
nav_order: 10
---

# Next Steps & Advanced Usage

### Running Multiple Jobs

GNPS Local supports multiple simultaneous jobs — just submit them from the web UI. Jobs run in background threads and do not block each other. Be aware that large jobs will compete for CPU resources.

### Exporting for External Analysis

- **Cytoscape (.graphml)**: Visualize and style the molecular network. The Cytoscape GNPS plugin (available in the Cytoscape App Store) can apply pre-built GNPS visual styles.
- **R/Python (.tsv files)**: `clusterinfo_summary_enriched.tsv` and `librarysearch_results_db.tsv` are standard tab-separated tables readable by any statistics tool.
- **Excel**: All `.tsv` output files open directly in Excel via File → Open.

### Checklist Before Analyzing Your Own Data

- [ ] Feature table exported from your software in the correct format (see Section 9)
- [ ] Feature table and MGF from the same software run (scan numbers must match)
- [ ] Metadata filename column exactly matches feature table sample names
- [ ] Single merged MGF file (not one file per sample)
- [ ] GNPS spectral library `.mgf` file(s) placed in:
  - **Windows WSL2:** `/mnt/d/GNPS_Local/libraries/`
  - **macOS:** `~/GNPS_Local/libraries/`

### Spectral Libraries

Download updated GNPS spectral libraries from:
```
https://gnps-external.ucsd.edu/gnpslibrary
```

Place any downloaded `.mgf` files directly into:

**Windows WSL2:**
```
/mnt/d/GNPS_Local/libraries/
```

**macOS:**
```
~/GNPS_Local/libraries/
```

The library is loaded automatically for every job.

### What Is Not Yet Implemented

The following features from cloud GNPS are not yet available locally:

- Dereplicator+ (peptidic natural product annotation)
- QIIME2 beta-diversity / PCoA statistics
- ili 3D spatial mapping
- MassIVE dataset search
- Automatic method descriptions

These may be added in future versions.