---
layout: default
title: Data Format Reference
nav_order: 9
---

# Data Format Reference

### Feature Quantification Table

The feature table must be a **comma-separated (.csv)** file with at minimum these columns:

| Column name | Example | Notes |
|---|---|---|
| `row ID` | `1`, `2`, `3` | Integer, must match SCANS= in MGF |
| `row m/z` | `256.0843` | Precursor m/z |
| `row retention time` | `1.245` | In minutes |
| `Sample1.mzML Peak area` | `45231` | One column per sample, exactly this format |

**First three rows example:**
```
row ID,row m/z,row retention time,Sample1.mzML Peak area,Sample2.mzML Peak area
1,256.0843,1.245,45231,12450
2,431.2012,3.812,0,98320
3,189.0558,2.104,22100,22050
```

**Common mistakes:**
- Column headers must be exact (case-sensitive). `Row ID` ≠ `row ID`.
- Sample columns must end in ` Peak area` (with a space before "Peak").
- Empty intensity cells should be `0`, not blank.

---

### Metadata Table

The metadata file must be a **tab-separated (.tsv)** file.

| Column name | Example | Notes |
|---|---|---|
| `filename` | `Sample1.mzML` | Must exactly match feature table sample names |
| `ATTRIBUTE_Group` | `treatment` | Any column starting with `ATTRIBUTE_` becomes a group |

**First three rows example:**
```
filename	ATTRIBUTE_Group	ATTRIBUTE_Timepoint
Sample1.mzML	treatment	early
Sample2.mzML	control	early
Sample3.mzML	treatment	late
```

**Common mistakes:**
- The `filename` column values must exactly match (including extension and case) what appears in the feature table sample column headers.
- Do not use blank cells. Use `N_A` (with an underscore) for missing values.

---

### MS/MS Spectra (MGF)

Your MGF file should be exported directly from your feature-finding software (MZmine "Export feature list as MGF", XCMS, etc.). Each spectrum block must include:

```
BEGIN IONS
SCANS=1
PEPMASS=256.0843
CHARGE=1+
100.2 5432.1
150.3 8921.0
END IONS
```

The `SCANS=` value must match the `row ID` in your feature table.

If your software uses `FEATURE_ID=` instead of `SCANS=`, this is handled automatically for MZmine3 output.
