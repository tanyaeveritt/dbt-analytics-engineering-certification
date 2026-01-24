#

* Identifying and verifying any raw object dependencies
* Understanding core dbt materializations
* Conceptualizing modularity and how to incorporate DRY principles

Modularity is the degree to which a system's components may be separated and recombined, often with the benefit of flexibility and variety in use.

* Converting business logic into performant SQL queries

## Using commands such as run, test, docs and seed
All commands here http://docs.getdbt.com/category/list-of-commands
### Run
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
#### Optional Flags
**Full Refresh Run** - Ignores the incremental logic in the where statement of the model and run for all days in the source data set.
```sql 
dbt run --full-refresh
```
**Empty Run** - Building schema-only dry runs
```sql 
dbt run --empty
```

**Fail-fast Run** - Building schema-only dry runs
```sql 
dbt run --empty
```
Learn more at [dbt run - dbt documentation]([https://popsql.com/learn-dbt/dbt-run-command](https://docs.getdbt.com/reference/commands/run)
Learn more at [dbt run - popsql](https://popsql.com/learn-dbt/dbt-run-command)

----
### Test
```sql
# run data and unit tests
dbt test

# run only data tests
dbt test --select test_type:data

# run only unit tests
dbt test --select test_type:unit

# run tests for one_specific_model
dbt test --select "one_specific_model"

# run tests for all models in package
dbt test --select "some_package.*"

# run only data tests defined singularly
dbt test --select "test_type:singular"

# run only data tests defined generically
dbt test --select "test_type:generic"

# run data tests limited to one_specific_model
dbt test --select "one_specific_model,test_type:data"

# run unit tests limited to one_specific_model
dbt test --select "one_specific_model,test_type:unit"
```
---

### Docs
#### Ability to generate documentation for your data models

**1. Generate the documentation**
```sql 
dbt docs generate
```
**2. Serve it locally** Start a web server and open the documentation in your default web browser. You can navigate through the documentation to view information about your dbt project
```sql 
dbt docs serve
```
---
### Seed
#### Allows you to load CSV files (referred to as “seeds”) into your data warehouse. 
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
