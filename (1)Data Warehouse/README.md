# Data Warehouse (Phase 1)

**Turning messy CSVs into clean, business-ready data — built from scratch in SQL.**

This project is a small but realistic **data warehouse** built to show how data actually moves:
from raw files → trusted tables → analytics-ready models.

Three layers. One clear flow.

**Bronze → Silver → Gold**

---

## The Layers (What each one does)

### 🥉 Bronze — Raw Data
- CSVs, ERP exports, CRM tables.
- No cleaning. No assumptions.
- Duplicates, bad dates, inconsistencies are expected.

**Purpose:**  
Keep the original data untouched.  
If something breaks downstream, Bronze is the source of truth.

---

### 🥈 Silver — Clean & Conformed
- Deduplication
- Date fixes and validation
- Standardized codes (gender, country, product lines)
- Trim unwanted spaces
- Business rules applied
- `dwh_create_date` added for traceability

**Purpose:**  
Create a **trusted, clean layer** that can safely be joined and modeled.

Silver is where data quality actually starts.

---

### 🥇 Gold — Business Ready
- Star schema design
- Dimensions + fact table
- Surrogate keys
- Clean, readable column names
- Built specifically for analytics and reporting

**Purpose:**  
This is the layer dashboards, reports, and models would query.

---

## How It Works (End-to-End)

1. **Initialize database**  
   Creates the `DWH` database with `bronze`, `silver`, and `gold` schemas.

2. **Load Bronze**  
   Raw CSVs are bulk inserted exactly as received.

3. **Transform to Silver**  
   Bronze data is cleaned, standardized, and validated.

4. **Build Gold Views**  
   Data is modeled into:
   - `dim_customers`
   - `dim_products`
   - `fact_sales`

At no point does data skip a layer.

---

## Data Flow Diagram

+----------------+ | Bronze | | Raw / Source | +--------+-------+ | v +----------------+ | Silver | | Clean / Trusted| +--------+-------+ | v +----------------+ | Gold | | Business Ready | +----------------+

---


**Legend**
- **Bronze:** Raw CSVs & ERP/CRM extracts
- **Silver:** Cleaned, standardized, validated
- **Gold:** Star schema for analytics

---

## Quality Checks (Guardrails)

Quality checks are not optional — they’re built into the process.

### Silver Layer Checks

| Table | What’s Checked | Why |
|-----|---------------|-----|
| Customers | Nulls, duplicate PKs, spaces, gender & marital status | Reliable joins |
| Products | Nulls, duplicate PKs, negative cost, date order | Accurate product data |
| Sales | Invalid dates, sales ≠ qty × price, null/negative values | Trustworthy metrics |
| ERP Tables | Invalid dates, inconsistent categories | Clean reference data |

---

### Gold Layer Checks

| Object | Check | Why |
|------|------|-----|
| dim_customers | Surrogate key uniqueness | Dimension integrity |
| dim_products | Surrogate key uniqueness | Unique products |
| fact_sales | FK links to dimensions | No orphan facts |

If Gold fails checks, analytics stop.  
Bad data is surfaced — not hidden.

---

## What Can Go Wrong (And How It’s Handled)

- Duplicate customers  
  → resolved in Silver using clean, conformed logic

- Invalid or impossible dates  
  → converted to NULL and flagged

- Incorrect sales math  
  → validated using quantity × price

- Orphan fact records  
  → caught during Gold integrity checks

Each layer has **one responsibility**.  
Problems are handled where they belong.

---

## Why This Project Matters

This isn’t just SQL practice.

It shows:
- Understanding of **ETL flow**
- Awareness of **data quality issues**
- Proper **layered warehouse design**
- Clean **fact & dimension modeling**
- How raw data becomes **business-ready**

This is how data works in real systems — just at a smaller scale.

---

## Usage

1. Clone the repository  
2. Run `init_database.sql`  
3. Run Bronze scripts  
   - `ddl_bronze.sql`
   - `strd_prcd_bronze.sql`
4. Run Silver scripts  
   - `ddl_silver.sql`
   - `strd_prcd_silver.sql`
5. Run `ddl_gold.sql`  
6. Query Gold views

That’s it.

---

## What’s Next

This warehouse is designed to be extended.

Next phases will:
- Add analytical use cases on top of Gold
- Combine multiple projects into one end-to-end system
- Show how data flows from ingestion → insight

Solid fundamentals first. Everything builds from here.
