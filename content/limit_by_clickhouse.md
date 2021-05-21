+++
title = "LIMIT BY statement in clickhouse"

date = 2021-05-21

[taxonomies]
tags = ["sql", "clickhouse"]
+++

https://clickhouse.tech/docs/en/sql-reference/statements/select/limit-by/

Learnt a nice feature of clickhouse at work today.

Say if you have a field like `httpHost` and you want to see up to 100 unique `paths` for each host, you can use the `LIMIT BY` statement to help you do that.

Example

```sql
SELECT 
   httpHost,
   path,
   count(*) as requestCount
FROM
   requests
GROUP BY
   httpHost,
   path
ORDER BY
  httpHost,
  requestCount DESC
LIMIT 100 BY httpHost
```
