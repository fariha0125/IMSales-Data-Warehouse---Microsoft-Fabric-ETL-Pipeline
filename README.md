# IMSales-Data-Warehouse---Microsoft-Fabric-ETL-Pipeline
Hands-on implementation of a dimensional data warehouse for IMSales, a B2B food trading company importing specialty products and selling to European retailers. 

### Business value: 
Enables sales by product/client/staff over time; inventory trends; regional analysis. 

## Core Skills:
Star schema design, Fabric Dataflows Gen2, Pipelines, SQL DW, data quality validation. 
### Skills Demonstrated
- Dimensional modeling (star schema, hierarchies, grains).
- Microsoft Fabric: Lakehouse, Dataflows Gen2, Pipelines, SQL DW.
- ETL best practices: Staging, DQ logging, varied activities (Copy + Dataflow).
- SQL: DDL, surrogate keys, constraints.

## Project Overview
- **Source**: IMSALES OLTP (Orders, Order Details, Clients, Products, etc. ~20-50k rows).
- **DW**: Fabric SQL Warehouse with surrogate keys, hierarchies enabled.
- **ETL**: Full pipeline from raw → staging → DW with quality checks.

## Architecture
The database structure is a star schema which consist of the below tables. 

<img width="1342" height="1198" alt="dw star schema" src="https://github.com/user-attachments/assets/ae1c6f7a-a4f7-4866-ad57-4bbe6ccd7aca" />



### The Fact table measures 
| Table          | Grain                                          | Measures                                                        |
| -------------- | ---------------------------------------------- | --------------------------------------------------------------- |
| fact_sales     | Order line (date–product–client–staff–shipper) | sales_unit_price, sales_unit_qty, sales_discount_perc           |
| fact_inventory | Product per date                               | cost_units_stocked, qty_units_stocked                    ​       |

### Dimension table hierarchies 
- dim_date: Day/Month/Quarter/Year; weekdays, semesters.
- dim_client: City/Country.
- dim_product: Product/Type/Supplier Country.
- dim_staff: Territory/Region/Country; age/seniority.
- dim_shipper: Coverage.

## Fabric Implementation 
**Workspace**: Project1_IMSALES 
<img width="2776" height="616" alt="Workspace IMSALES" src="https://github.com/user-attachments/assets/4c5dd85c-4167-4e81-96b9-5bcf1aa84362" />

**Source Data**
<img width="1764" height="764" alt="Source data" src="https://github.com/user-attachments/assets/3f0dc45d-f6ec-4465-a9f3-b965c112f325" />

<img width="1546" height="1004" alt="Source csv files" src="https://github.com/user-attachments/assets/a3295d0b-d643-4bd9-91b2-9cc89f0a7849" />
<br><br><br> 

**Staging Area**:
<img width="1768" height="712" alt="Staging Area IMSALES" src="https://github.com/user-attachments/assets/7f5286b8-67fc-4348-b266-46128f7832bd" />

- STG_PROJECT1_IMSALES DW
- Pipelines:
- Key Dataflows 

## Data Quality & Transformation 
**4 validation rules** logged to log_quality_checks:
1.	Business Key (PK) integrity per dim.
2.	Dimension row uniqueness.
3.	Fact composite FK (PK) uniqueness.
4.	Referential integrity (fact FK → dim BK).

**Transformations** (Dataflow Gen2):
•	Joins (Orders → Order Details).
•	Derived measures (discount as %).
•	Type conversions, null handling.
•	Surrogate key prep.

## Run Locally 
1.	Fabric → New workspace, import structure.
2.	Load source CSVs to Lakehouse.
3.	Execute: STG Load → Validate → DW Load.
4.	Query: SELECT * FROM fact_sales (sample matches).

## Files 

## Next Steps 
•	Power BI semantic model + dashboards.





