## QA Cheat Sheet – Silver & Gold Layers

| Layer  | Table                  | What We're Checking                                     | Why It Matters |
|--------|-----------------------|--------------------------------------------------|----------------|
| Silver | crm_cust_info          | PK duplicates/nulls, unwanted spaces, gender & marital status standardization | Clean customer data, no duplicates, ready for joins |
| Silver | crm_prd_info           | PK duplicates/nulls, negative/null cost, unwanted spaces, product line consistency, date order | Products are accurate & reliable for analytics |
| Silver | crm_sales_details      | Invalid dates, order/ship/due sequence, sales ≠ qty*price, nulls/negative | Sales facts are consistent & ready for aggregation |
| Silver | erp_cust_az12          | Out-of-range birthdates, gender normalization | Accurate demographic info |
| Silver | erp_loc_a101           | Country normalization | Locations are standardized for joins |
| Silver | erp_px_cat_g1v2        | Unwanted spaces, maintenance normalization | Product categories clean and consistent |
| Gold   | dim_customers          | Surrogate key uniqueness | Ensures dimensions are reliable for facts |
| Gold   | dim_products           | Surrogate key uniqueness | Ensures products are unique for facts |
| Gold   | fact_sales             | Referential integrity with dim_customers & dim_products | Facts correctly linked, no orphan records |
