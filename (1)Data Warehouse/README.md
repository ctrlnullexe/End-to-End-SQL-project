# Data Warehouse

**Turn messy CSVs into clean, business-ready insights, built from scratch in SQL.**


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

## QA Cheat Sheet (Simplified)

| Layer  | Table             | Key Checks                         | Why It Matters                  |
|--------|-----------------|-----------------------------------|--------------------------------|
| Silver | Customers        | PK duplicates/nulls, spaces, gender/marital status | Clean, reliable for joins |
| Silver | Products         | PK duplicates/nulls, cost ≥ 0, date order | Accurate product info        |
| Silver | Sales Details    | Invalid dates, sales ≠ qty*price | Sales facts are consistent    |
| Gold   | dim_customers    | Surrogate key uniqueness          | Dimension table integrity      |
| Gold   | dim_products     | Surrogate key uniqueness          | Products are unique            |
| Gold   | fact_sales       | FK links to dimensions            | Facts linked correctly         |

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


