<!--
{% comment %}
Licensed to Julian Hyde under one or more contributor license
agreements.  See the NOTICE file distributed with this work
for additional information regarding copyright ownership.
Julian Hyde licenses this file to you under the Apache
License, Version 2.0 (the "License"); you may not use this
file except in compliance with the License.  You may obtain a
copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
either express or implied.  See the License for the specific
language governing permissions and limitations under the
License.
{% endcomment %}
-->
# foodmart-data
Foodmart data set as CSV files.

This project contains the Foodmart data set as CSV files, one per
table.

It originated as part of the test suite of the
[Mondrian OLAP engine](https://github.com/pentaho/mondrian).

## Schema

Foodmart contains 26 tables:
* 7 fact tables: sales_fact_1997, sales_fact_1998, sales_fact_dec_1998,
  inventory_fact_1997, inventory_fact_1998, salary, expense_fact
* 19 dimension tables: product, customer, time_by_day, employee and more

Together they hold 328,060 rows, about 15MB uncompressed.

There is a
[schema diagram](https://github.com/julianhyde/foodmart-data-hsqldb/blob/main/foodmart-schema.png)
in the foodmart-data-hsqldb project; note that it also shows the
aggregate tables, which this project does not include (see
[below](#aggregate-tables)).

## The files

Each table is a file `csv/<table>.csv`. The first line is a header row
of column names; the remaining lines are data rows, quoted according to
[RFC 4180](https://www.rfc-editor.org/rfc/rfc4180). An empty field
represents SQL NULL.

```
$ head -3 csv/days.csv
day,week_day
1,Sunday
2,Monday
```

The column types are those of the
[foodmart-data-hsqldb](https://github.com/julianhyde/foodmart-data-hsqldb)
project, from which these files are taken.
[tools/schema.py](tools/schema.py) lists every table and column, with
its type and whether it is nullable.

## Aggregate tables

The Foodmart data set also has 11 aggregate tables, whose names start
with `agg_`. This project does not include them: they are 60% of the
data by size, and each is a `GROUP BY` rollup of `sales_fact_1997`, so
you can compute any of them from the data that is here. For example,
`agg_l_03_sales_fact_1997` is

```sql
SELECT "time_id", "customer_id",
    SUM("store_sales"), SUM("store_cost"), SUM("unit_sales"), COUNT(*)
FROM "sales_fact_1997"
GROUP BY "time_id", "customer_id"
```

If you need the aggregate tables as data, use
[foodmart-data-hsqldb](https://github.com/julianhyde/foodmart-data-hsqldb).

## Get foodmart-data

```bash
$ git clone https://github.com/hydromatic/foodmart-data.git
```

## See also

The same data set in other formats:
* [foodmart-data-hsqldb](https://github.com/julianhyde/foodmart-data-hsqldb)
  &mdash; an embedded HSQLDB database, for Java; includes the aggregate
  tables
* [foodmart-data-json](https://github.com/julianhyde/foodmart-data-json)
  &mdash; JSON
* [foodmart-data-mysql](https://github.com/julianhyde/foodmart-data-mysql)
  &mdash; MySQL
* [foodmart-queries](https://github.com/julianhyde/foodmart-queries)
  &mdash; a set of queries against this data set

Similar data sets:
* [chinook-data-hsqldb](https://github.com/julianhyde/chinook-data-hsqldb)
* [flight-data-hsqldb](https://github.com/julianhyde/flight-data-hsqldb)
* [look-data-hsqldb](https://github.com/hydromatic/look-data-hsqldb)
* [sakila-data-hsqldb](https://github.com/hydromatic/sakila-data-hsqldb)
* [scott-data-hsqldb](https://github.com/julianhyde/scott-data-hsqldb)
* [steelwheels-data-hsqldb](https://github.com/julianhyde/steelwheels-data-hsqldb)

## More information

* **License:** Apache License, Version 2.0
* **Author:** [Julian Hyde](https://github.com/julianhyde)
  ([@julianhyde](https://twitter.com/julianhyde))
* **Blog:** http://blog.hydromatic.net
* **Source code:** https://github.com/hydromatic/foodmart-data
* **Issues:** https://github.com/hydromatic/foodmart-data/issues
* **Release notes:** [CHANGELOG.md](CHANGELOG.md)

<!-- End README.md -->
