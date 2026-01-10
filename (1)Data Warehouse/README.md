# SQL Data Warehouse Project

Turn messy CSVs into clean, business-ready insights — built from scratch in SQL.

---

## Layers

### 🥉 Bronze – Raw Data
- Original CSVs and ERP/CRM exports.
- May have duplicates, nulls, messy codes.
- Purpose: Keep raw source intact as fallback.

### 🥈 Silver – Clean & Trusted
- Deduplicated, trimmed, standardized.
- Dates fixed, codes normalized, nulls handled.
- Purpose: Reliable, clean tables ready for analysis.

### 🥇 Gold – Business-Ready
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

> **Tip:** You don’t need to know every SQL function — just know the **layer purpose**, **flow**, and **why we check for duplicates/nulls**.

---

## QA Cheat Sheet (Simplified)

| Layer  | Table             | Key Checks                         | Why It Matters                  |
|--------|-----------------|-----------------------------------|--------------------------------|
| Silver | Customers        | PK duplicates/nulls, spaces, gender/marital status | Clean, reliable for joins |
| Silver | Products         | PK duplicates/nulls, cost ≥ 0, date order | Accurate product info        |
| Silver | Sales Details    | Invalid dates, sales ≠ qty*price | Sales facts are consistent    |
| Gold   | dim_customers    | Surrogate key uniqueness          | Dimension table integrity      |
| Gold   | dim_products     | Surrogate key uniqueness          | Products are unique            |
| Gold   | fact_sales       | FK links to dimensions            | Facts linked correctly         |

> **Pro tip:** Focus on **flow and purpose**, not every SQL line. That’s what recruiters want to see.

---

## Data Flow Diagram


