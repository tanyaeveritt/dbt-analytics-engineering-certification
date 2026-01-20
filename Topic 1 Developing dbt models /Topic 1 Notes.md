#


* Identifying and verifying any raw object dependencies
* Understanding core dbt materializations
* Conceptualizing modularity and how to incorporate DRY principles
* Converting business logic into performant SQL queries
* Using commands such as run, test, docs and seed

## Run
**Run all models** 
```sql
dbt run
```

**Run one model** - file name is sales.sql
```sql
dbt run --model sales
```
OR
```sql
dbt run -m sales
```

**Full Refresh Run** - Ignores the incremental logic in the where statement of the model and run for all days in the source data set.
```sql 
dbt run --model sales --full-refresh
```
Learn more at [dbt run - dbt documentation](https://popsql.com/learn-dbt/dbt-run-command)

----
## Test
```dbt test```

---

## Docs
### Ability to generate documentation for your data models

**1. Generate the documentation**
```sql 
dbt docs generate
```
**2. Serve it locally** Start a web server and open the documentation in your default web browser. You can navigate through the documentation to view information about your dbt project
```sql 
dbt docs serve
```
---
## Seed
### Allows you to load CSV files (referred to as “seeds”) into your data warehouse. 
Static referenece data in csv format\
Place seed file in the **seed folder** directory of your dbt project.

**Load all seed files** into Your Data Warehouse
```sql
dbt seed
```
**Load one seed file** file name product_codes.csv
```sql
dbt seed --select product_codes
```
**Reference in model files**
```
{{ ref('product_codes') }}
```

```sql
select    
  orders.*,    
  product_codes.product_name

from {{ ref('orders') }} as orders

  left join {{ ref('product_codes') }} as product_codes
    on orders.product_code = product_codes.product_code
```

Learn more at [dbt seed - dbt documentation](https://popsql.com/learn-dbt/dbt-seed)


---
* Creating a logical flow of models and building clean DAGs
* Defining configurations in dbt_project.yml
* Configuring sources in dbt
* Using dbt Packages
* Utilizing git functionality within the development lifecycle
* Creating Python models
* Providing access to users to models with the “grants” configuration

```grants ```

[Grants - dbt documentation link](https://docs.getdbt.com/reference/resource-configs/grants)
