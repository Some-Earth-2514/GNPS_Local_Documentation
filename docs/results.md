---
layout: default
title: Understanding your Results
nav_order: 6
---

# Understanding your Results

### The Molecular Network

The network is a graph where:

- **Each node** = one MS/MS feature (a detected compound, or candidate compound) from your data
- **Each edge** = a cosine similarity score ≥ 0.7 (by default) between two spectra, meaning those two features probably share structural similarity
- **Connected clusters** = groups of structurally related compounds (e.g., a series of acyl chain variants)
- **Isolated nodes** (no edges) = features with no structurally similar neighbors in your dataset

A node annotated with a compound name (e.g., "Caffeic acid, MQScore=0.85") means that feature's fragmentation pattern closely matched a reference spectrum in the spectral library.

### Library Match Scores

The `MQScore` (Matching Quality Score) ranges from 0 to 1:

- **0.9–1.0**: Very confident match
- **0.7–0.9**: Good match; confirm with accurate mass
- **0.5–0.7**: Tentative match; treat as a lead, not a confirmed ID
- **< 0.5**: Usually not reported (filtered out by default threshold)

### Common Questions

**"Why is my network very sparse with few edges?"**
Most likely causes: cosine threshold too high (try lowering from 0.7 to 0.5), too few matched peaks (try lowering from 6 to 4), or genuine chemical diversity in your sample.

**"Why do I have very few library matches?"**
The GNPS spectral library covers primarily natural products and common metabolites. Novel compounds, lipids with unusual chains, or very small molecules often do not match. This is expected and does not indicate a pipeline error.

**"What does component index mean?"**
Nodes with the same component index belong to the same connected cluster in the network. `-1` means the node is a singleton (no edges).
