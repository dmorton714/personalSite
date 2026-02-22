The Problem

We needed to analyze sales performance for a single product across multiple retail locations using exports from a legacy Point of Sale (POS) system.

The core objectives were:
- Identify top customers by revenue and volume
- Rank store performance
- Calculate units sold per location
- Detect inconsistencies across reports
- Consolidate fragmented data into a reliable, structured dataset

The primary challenge was not analytics — it was data acquisition and normalization.
Reports were manually generated, inconsistently formatted, and separated across multiple sheets and stores.

To produce meaningful insights, we first needed to build a repeatable data pipeline.

---
---
---
---

#1 — Automated Data Extraction

The POS system did not provide an API, so I implemented a Selenium-based browser automation workflow to programmatically retrieve reports.

The automation:
- Authenticated into the POS web interface
- Navigated dynamic reporting views
- Triggered report generation
- Downloaded and organized exported files
- Standardized file naming conventions for downstream processing

This replaced a manual, multi-step workflow and reduced report collection time from hours to minutes.
(Automation component removed from public demo due to sensitive credentials.)

Key takeaway: When APIs don’t exist, automation becomes infrastructure.


#2 — Data Cleaning & Normalization

Each exported report contained structural inconsistencies:
- Redundant headers
- Irrelevant columns
- Store-specific formatting differences
- Mixed date and currency formats
- Inconsistent product labeling

Using Python (pandas), I built a cleaning pipeline that:
- Dropped non-essential columns
- Standardized schema across all stores
- Normalized date formats and numeric types
- Cleaned currency fields and unit counts
- Unified naming conventions
- Merged seven independent sheets into a single master dataset

The output was a normalized, analysis-ready dataframe with consistent structure across all locations.
This stage transformed raw exports into a reliable source of truth.







#3 — Analytical Layer & Reusable Metrics

With structured data in place, I implemented modular functions to compute key performance metrics:

Top customers by revenue
Top customers by units purchased
Revenue per store
Units sold per store
Distribution and ranking analysis
Time-based aggregation
Functions were written to be reusable and parameterized, allowing flexible filtering by store, date range, or customer.
This reduced analysis from manual spreadsheet inspection to deterministic, reproducible computations.
The result: scalable insight generation rather than one-off reporting.




#4 — Interactive Dashboard & Visualization

To surface insights for non-technical stakeholders, I built an interactive dashboard layer.

The dashboard:
Displays ranked store performance
Highlights high-value customers
Allows filtering and sorting
Visualizes sales distribution across locations
Presents clean, decision-ready metrics

This enabled management to:
Identify top-performing stores immediately
Detect underperformance
Adjust inventory strategy
Recognize customer purchasing patterns
The project shifted reporting from reactive spreadsheet review to proactive, data-driven decision support.

Engineering Impact

This project demonstrates:
Automation in environments without APIs
Practical data engineering and normalization
Analytical modeling using structured data
Clear separation between data pipeline and presentation layer
Building internal tooling to improve operational visibility

It began as a reporting problem.
It became a lightweight data pipeline with a decision-support interface.