# Topic 7: Implementing and maintaining external dependencies

## Implementing dbt exposures


## Implementing source freshness
source or model level
e.g. 
```sql
sources:
  - name: jaffle_shop
    database: raw
    config: 
      freshness: # default freshness
        warn_after: {count: 12, period: hour}
        error_after: {count: 24, period: hour}
      loaded_at_field: _etl_loaded_at # changed to config in v1.10

    tables:
      - name: orders
        config:
          freshness: # make this a little more strict
            warn_after: {count: 6, period: hour}
            error_after: {count: 12, period: hour}

      - name: customers # this inherits the default freshness defined in the jaffle_shop source block at the beginning

      - name: product_skus
        config:
          freshness: null # do not check freshness for this table
```
