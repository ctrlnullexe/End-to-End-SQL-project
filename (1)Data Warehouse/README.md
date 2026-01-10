# SQL Data Warehouse Project

Turn messy CSVs into clean, business-ready insights — built from scratch in SQL.

---

## Layers

### 🥉 Bronze (Raw Data)
- Original CSVs and ERP/CRM exports.
- May have duplicates, nulls, messy codes.
- Purpose: Keep raw source intact as fallback.

### 🥈 Silver (Clean & Trusted)
- Deduplicated, trimmed, standardized.
- Dates fixed, codes normalized, nulls handled.
- Purpose: Reliable, clean tables ready for analysis.

### 🥇 Gold (Business Ready)
- Star schema: **dimensions + fact table**.
- Surrogate keys, joined tables, ready for dashboards.
- Purpose: Analytics-ready, plug-and-play.

---

## How it works

1. `init_database.sql` → create DWH database + schemas  
2. `ddl_bronze.sql` + `strd_prcd_bronze.sql` → load raw data  
3. `ddl_silver.sql` + `strd_prcd_silver.sql` → clean & transform  
4. `ddl_gold.sql` → create dimensions & fact tables  
5. `qc_silver.sql` + `qc_gold.sql` → basic quality checks

---

## Quality Check Cheat Sheet

| Layer  | Table             | Key Checks                         | Why It Matters                  |
|--------|-----------------|-----------------------------------|--------------------------------|
| Silver | Customers        | PK duplicates/nulls, spaces, gender/marital status | Clean, reliable for joins |
| Silver | Products         | PK duplicates/nulls, cost ≥ 0, date order | Accurate product info        |
| Silver | Sales Details    | Invalid dates, sales ≠ qty*price | Sales facts are consistent    |
| Gold   | dim_customers    | Surrogate key uniqueness          | Dimension table integrity      |
| Gold   | dim_products     | Surrogate key uniqueness          | Products are unique            |
| Gold   | fact_sales       | FK links to dimensions            | Facts linked correctly         |



---

## Data Flow Diagram

    +----------------+
    |     Bronze     |
    |  Raw / Source  |
    +--------+-------+
             |
             v
    +----------------+
    |     Silver     |
    | Clean / Trusted|
    +--------+-------+
             |
             v
    +----------------+
    |      Gold      |
    | Business-Ready |
    +----------------+


---

## How Data Moves Through the System

This warehouse is designed to mirror how data flows in real systems.

1. **Source data arrives** as CSVs (CRM, ERP).
2. Data is loaded **as is** into Bronze (no changes).
3. Bronze data is **cleaned and standardized** in Silver.
4. Silver data is **modeled for analytics** in Gold.
5. Gold data is validated before use.

Each layer has a single responsibility.

---

## What Can Go Wrong (and how it’s handled)

- Duplicate customers → handled in Silver using latest records
- Invalid dates → converted to NULL
- Incorrect sales values → recalculated using quantity × price
- Orphan records → caught in Gold quality checks

Quality checks act as guardrails before data is used.

---

## Why This Project Matters

It shows:
- Understanding of the ETL flow
- Awareness of data quality issues
- Proper layered warehouse design
- Clean fact & dimension modeling
- How raw data becomes business ready

This is how data works in real systems (just at a smaller scale).

---

## Usage

1. Clone repo  
2. Run `init_database.sql`  
3. Run `ddl_bronze.sql` → `strd_prcd_bronze.sql`  
4. Run `ddl_silver.sql` → `strd_prcd_silver.sql`  
5. Run `ddl_gold.sql`  
6. Run `qc_silver.sql` + `qc_gold.sql` (optional but recommended)  
7. Query Gold views. Done.
