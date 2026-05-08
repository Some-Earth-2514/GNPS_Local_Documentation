---
layout: default
title: Workflow Details
nav_order: 8
---

# Workflow Details

### What FBMN Actually Does

Your data goes through these stages in order:

1. **Metadata merge** — Your sample metadata is loaded and linked to file names.
2. **Input validation** — Column names and file formats are checked; warnings are logged but the pipeline continues.
3. **Quantification reformatting** — Your feature table (MZmine/XCMS/MS-DIAL format) is converted to the internal GNPS format.
4. **Spectra filtering** — Peaks within the precursor isolation window are removed, and a noise filter is applied. This improves cosine score quality.
5. **Molecular networking** — Every pair of spectra is compared by cosine similarity. Pairs above the threshold become edges.
6. **Edge filtering** — Each node keeps only its top-K best edges; components exceeding the maximum size are pruned.
7. **Library search** — Each spectrum is compared against the local GNPS spectral library.
8. **Cluster info summary** — Features, quantification values, and metadata are merged into a single table.
9. **Enrichment** — Library hits and component indices are added to the cluster info table.
10. **GraphML export** — Everything is assembled into a single file readable by Cytoscape.

### Key Parameters and When to Change Them

| Parameter | Default | What it does | When to change |
|---|---|---|---|
| Cosine Score Threshold | 0.7 | Minimum similarity for an edge | Lower to 0.5 for exploratory analysis; raise to 0.85 for validation |
| Min Matched Peaks | 6 | Minimum shared fragment ions for an edge | Lower to 4 for low-quality spectra; raise to 8 for high confidence |
| Top K Edges per Node | 10 | Max neighbors per feature | Lower for cleaner networks; raise for community detection |
| Max Component Size | 100 | Largest allowed cluster | Set to 0 (unlimited) if you want to see full propagation |
| Fragment Tolerance | 0.02 Da | m/z window for matching fragment ions | Raise to 0.05 for ion-trap data; keep at 0.02 for Orbitrap/Q-TOF |

### Current Limitations

- **Analog search** is implemented in the pipeline but awaiting verification.
- **Statistical analysis** (volcano plots, PCoA) requires the `RUN_STATS` parameter and is not yet enabled in the UI.
- **QIIME2 integration** and **ili 3D spatial mapping** are not available in the local version.
- Only **one MGF file** is supported per job (multi-file input must be merged upstream).
