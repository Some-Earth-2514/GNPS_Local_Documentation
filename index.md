---
layout: default
title: Home
nav_order: 1
description: "Introduction to GNPS Local"
---

# GNPS Local

GNPS Local is an offline version of the GNPS (Global Natural Products Social Molecular Networking) platform — the widely-used tool for annotating small molecules in MS/MS metabolomics data. Where the original GNPS ran on cloud servers at UC San Diego, GNPS Local runs entirely on your own computer, with no internet connection needed once it is set up.

The core workflow supported is **Feature-Based Molecular Networking (FBMN)**. You bring your MS/MS spectra and a feature quantification table (from MZmine, XCMS, MS-DIAL, or similar), and GNPS Local builds a molecular network: a visual map in which each node is a detected feature and edges connect features with similar fragmentation patterns. Nodes that match known compounds in the spectral library are annotated automatically.

This tool is designed for researchers who already understand molecular networking concepts and want results without waiting for cloud job queues, without sharing data externally, or without an internet connection. Think of it as running the GNPS analysis server on your own laptop — same science, same outputs, fully local.

---
# Why should you use GNPS Local?

![testing]({{ site.baseurl }}/assets/images/Performance.png)

Benchmark testing shows that consumer laptops can achieve computing performace **better than GNPS** with more library hits, all offline with zero network dependency while your **data stays completely private**. 

> NOTE: Testing was done using 100 open source spectral libraries and same parameters across all runs with only difference in computer hardware specifications.

*unpruned with cosine score = 0.1<br>
**pruned with cosine socre = 0.7