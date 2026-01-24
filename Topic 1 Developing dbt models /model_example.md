## What does a model file looks like 


## Model file example using source 
```sql
--Filename: orders.sql

select
  ...

from {{ source('jaffle_shop', 'orders') }}

left join {{ source('jaffle_shop', 'customers') }} using (customer_id)
```

## Model file example using reference 
```sql
--Filename: sales.sql

{{ config(
materialized='incremental'
) }}

select 
  sales_date,
  product_category, 
  sum(sales_amount) as total_sales, 
  avg(sales_amount) as average_sales, 
  count(*) as number_of_transactions

from {{ref('stg_sales_data')}} 

{% if is_incremental() %}

  where sales_date > (select max(sales_date) from {{ this }})

{% endif %}

group by sales_date, product_category
```
