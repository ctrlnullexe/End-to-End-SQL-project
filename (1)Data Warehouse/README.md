# Data Warehouse
# SQL Data Warehouse Project

![SQL](https://img.shields.io/badge/Tech-SQL-blue)
![Bronze](https://img.shields.io/badge/Bronze-Raw-orange)
![Silver](https://img.shields.io/badge/Silver-Clean-green)
![Gold](https://img.shields.io/badge/Gold-Business-ready-brightgreen)
![Status](https://img.shields.io/badge/Status-Working-brightgreen)

A **SQL data warehouse built from scratch**. Clean, practical, and shows I understand **how raw data becomes business-ready insights**.

Three layers: **Bronze → Silver → Gold**. Each has a role.

---

## Layers

### 🥉 Bronze – Raw Data
- CSVs, ERP exports, CRM tables.
- Unprocessed. Messy. Duplicates possible.
- Purpose: Keep the original source intact. Always a fallback.

### 🥈 Silver – Clean & Conformed
- Deduplicate, fix dates, standardize codes, trim spaces.
- Add `dwh_create_date` for tracking.
- Purpose: Trusted layer for transformations and joins.

### 🥇 Gold – Business-ready
- Star schema: **dimensions + fact table**.
- Surrogate keys, clean names, joined tables.
- Purpose: Analytics-ready. Plug into dashboards, reports, or models.

---

## How it works

1. **Init database** → creates `DWH` with bronze, silver, gold schemas.  
2. **Load Bronze** → bulk insert CSVs into bronze tables.  
3. **Load Silver** → ETL from bronze → silver (clean, dedupe, transform).  
4. **Gold Views** → dim_customers, dim_products, fact_sales. Ready to query.

---

## Why it matters

- Shows **full ETL understanding**.  
- Data traceable from raw → clean → business-ready.  
- Layers separate so **raw data never gets corrupted**.  
- Mini warehouse to practice real-world analytics, BI, or ML.

---

## Quick Reference

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
    

**Legend:**  
- **Bronze:** Original, messy CSVs & ERP/CRM tables.  
- **Silver:** Deduped, standardized, cleaned.  
- **Gold:** Star schema, ready for dashboards & analytics.  


---

## Usage

1. Clone repo  
2. Run `init_database.sql`  
3. Run `ddl_bronze.sql` → `strd_prcd_bronze.sql`  
4. Run `ddl_silver.sql` → `strd_prcd_silver.sql`  
5. Run `ddl_gold.sql`  
6. Query Gold views. Done.


