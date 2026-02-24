# JKN Claims Warehouse

A reproducible analytic data warehouse for Indonesian National Health Insurance (JKN) claims data.

This repository contains the SQL transformation layer that converts raw administrative claims into standardized analytic datasets suitable for health services research, audit, and policy monitoring.

---

## Purpose

Administrative claims data are not directly analyzable.
They are event-based billing records, not clinical episodes.

The JKN Claims Warehouse restructures claims into research-ready constructs:

* patient care episodes
* revisit intervals
* referral patterns
* provider fragmentation
* abnormal utilization signals

This enables population-level analysis without accessing medical records.

---

## Architecture

The system is part of a larger research platform:

R pipeline (jkn-data-platform) → BigQuery warehouse → Analytic marts → Research studies

This repository implements the **warehouse layer**.

---

## Data Layers

### 1. Raw Layer (`00_raw`)

External data ingested from administrative claim extracts.

No transformation applied.

### 2. Staging Layer (`01_staging`)

Data cleaning and normalization:

* de-duplication of visits
* standardization of patient identifiers
* provider normalization
* episode ordering

### 3. Fragmentation & Episode Layer (`fragmentasi`)

Construction of analytic units:

* revisit within 7 days
* inter-provider switching
* referral reset
* continuity of care

### 4. Mart Layer (`02_mart`)

Research-ready tables:

* episode-based utilization
* provider-level indicators
* audit detection outputs

---

## Research Applications

The warehouse supports multiple studies:

* obstetric claim anomaly detection
* referral fragmentation analysis
* catastrophic cost prediction
* strategic purchasing monitoring

---

## Reproducibility

All transformations are SQL-based and deterministic.

Given the same raw claim extract, the warehouse rebuilds identical analytic datasets.

No patient-level data is included in this repository.

---

## How it is executed

The warehouse is executed via the companion repository:

`jkn-data-platform`

Run:

```r
source("pipeline/run_data_platform.R")
```

---

## Contribution

This project proposes a framework for using national insurance administrative data as a popul
