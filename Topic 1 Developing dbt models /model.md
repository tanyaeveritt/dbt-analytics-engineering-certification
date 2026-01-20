## What does a model file looks like 

```sql
--Filename: sales.sql

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
