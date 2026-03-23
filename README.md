# IMSales-Data-Warehouse---Microsoft-Fabric-ETL-Pipeline
Hands-on implementation of a dimensional data warehouse for IMSales, a B2B food trading company importing specialty products and selling to European retailers. 
**Business value**: Enables sales by product/client/staff over time; inventory trends; regional analysis. 

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
The database structure is a star schema structure which consist of teh below tables. 

<img width="1584" height="846" alt="image" src="https://github.com/user-attachments/assets/148b2399-4ac0-4e50-91dc-e15231e068b2" />

The Fact table measures and Diemnsion table hierarchies details can be found here (add link)

## Fabric implementation 
- Workspace:
- Staging:
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





