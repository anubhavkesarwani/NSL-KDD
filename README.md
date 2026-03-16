# NSL-KDD Dataset — Cleaned for NIDS Research

| Property | Value |
|----------|-------|
| Records (cleaned) | 140,788 |
| Columns | 38 |
| Features | 35 network features |
| Classes | Binary (BENIGN / ATTACK) + 5 attack categories |

## Attribution

> Tavallaee, M., Bagheri, E., Lu, W., & Ghorbani, A. (2009). *A detailed analysis of the KDD CUP 99 data set*. IEEE Symposium on Computational Intelligence for Security and Defense Applications (CISDA).

Dataset source: [University of New Brunswick](https://www.unb.ca/cic/datasets/nsl.html)

---

## Preparation Pipeline

Cleaning is performed using a single Python script with **pandas** and **numpy**.

Main operations:

- Merge `KDDTrain` and `KDDTest`
- Remove redundant column (`classnum`)
- Strip whitespace and eliminate invalid values
- Standardize column names
- Convert strings to categorical types
- Normalize benign label (`normal → BENIGN`)
- Map individual attacks to NSL-KDD attack categories
- Create binary label (`Label`: 0 = BENIGN, 1 = ATTACK)
- Remove constant columns
- Remove duplicate rows
- Validate dataset integrity (no NaNs, no duplicates)

---

## Dataset Structure

```
35 network traffic features
Attacktype       Attack category (BENIGN / DoS / Probe / R2L / U2R)
Class            Specific attack name or BENIGN
Label            Binary label (0 benign, 1 attack)
```

---

## Class Distribution

| BENIGN | ATTACK | BENIGN % | ATTACK % |
|--------|--------|----------|----------|
| 75,959 | 64,829 | 53.96% | 46.04% |

### Attack Category Distribution

| Category | Records |
|---------|---------|
| DoS | 51,363 |
| Probe | 9,805 |
| R2L | 3,542 |
| U2R | 119 |

---

## Feature Characteristics

Categorical features:

| Feature | Unique values |
|--------|---------------|
| Protocol_type | 3 |
| Service | 70 |
| Flag | 11 |

All other features are numeric network flow statistics used for intrusion detection.

---

## Data Quality Validation

The cleaned dataset passes the following integrity checks:

| Check | Result |
|------|-------|
| Missing values | 0 |
| Infinite values | 0 |
| Duplicate rows | 0 |
| Duplicate columns | 0 |
| Constant columns | Removed (`num_outbound_cmds`) |
| Redundant column | Removed (`classnum`) |

All categorical fields were normalized and stripped of whitespace before validation. Numeric features were converted to appropriate numeric types and verified to contain valid values.

---

## Files

```
nsl_kdd.csv
```

Cleaned NSL-KDD dataset ready for machine-learning experiments.

---

## Downstream Responsibilities

The following steps belong in the ML pipeline rather than dataset preparation:

- Encoding categorical features (`Protocol_type`, `Service`, `Flag`)
- Train/test splitting
- Feature scaling
- Class imbalance handling

---

## References

1. Tavallaee, M., Bagheri, E., Lu, W., & Ghorbani, A. (2009). *A detailed analysis of the KDD CUP 99 data set*. IEEE CISDA.
2. Arp, D. et al. (2022). *Dos and don'ts of machine learning in computer security*. USENIX Security.

---

## License

NSL-KDD original licensing terms apply. Academic use requires attribution to Tavallaee et al. (2009).
