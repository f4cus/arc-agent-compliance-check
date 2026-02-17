# Azure Arc Coverage Validation — Streamlit Dashboard

## Problem

In hybrid environments, validating Azure Arc agent coverage across servers becomes repetitive and error-prone when done manually.

The typical approach involves exporting the full CMDB and comparing it against a CSV export from Azure Arc. When this process is handled through spreadsheets and pivot tables, small filtering mistakes or inconsistent naming can produce incorrect compliance reports.

Over time, this leads to unreliable visibility of which servers are actually reporting to Azure Arc.

---

## Context

This tool was built to support a recurring operational task:

- Validate that all eligible servers have the Azure Arc agent installed.
- Detect servers reporting as Offline or Expired.
- Identify servers present in CMDB but missing from Azure Arc.
- Generate filtered reports for remediation tracking.

The environment assumes:

- A structured CMDB export (Excel).
- An Azure Arc CSV export from the portal.
- Enterprise-scale datasets where manual validation does not scale reliably.

---

## Solution

This application provides a consistent, repeatable validation process by:

- Normalizing both data sources.
- Performing a controlled merge between CMDB and Azure Arc datasets.
- Classifying servers based on agent status.
- Allowing dynamic filtering for targeted reporting.
- Exporting results for operational follow-up.

The objective is not to replace Azure governance tools, but to eliminate manual reconciliation errors.

---

## Architecture / Approach

- Python for data processing.
- Pandas for deterministic dataset merging.
- Streamlit for interactive filtering and review.
- Explicit column normalization to reduce mismatch caused by naming inconsistencies.

Design choices:

- Keep the logic transparent and maintainable.
- Avoid unnecessary infrastructure dependencies.
- Prioritize clarity over abstraction.
- Build for operational repetition, not one-time analysis.

This is a lightweight internal validation tool, not a platform.

---

## Operational Considerations

- Accuracy depends on CMDB data quality.
- Hostname consistency is critical for reliable matching.
- Azure Arc exports must contain stable identifiers.
- Designed for structured enterprise datasets.

This tool improves visibility, but governance maturity still depends on process discipline.

---

## Usage

Requirements:
- Python 3.x

Setup:
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
streamlit run app.py
---
Example datasets included:

- `cmdb.xlsx` (Sheet: `INFRAESTRUCTURA`)
- `AzureArc.csv` (Columns: `HOST NAME`, `NAME`, `ARC AGENT STATUS`)

Both files must be placed in the same directory as `app.py`.

---

## Lessons Learned

- Spreadsheet-based reconciliation does not scale operationally.
- Small filtering mistakes can invalidate compliance reports.
- Data normalization is often more important than visualization.
- Lightweight tooling can significantly reduce recurring manual effort.
- Visibility issues are frequently procedural, not technical.

