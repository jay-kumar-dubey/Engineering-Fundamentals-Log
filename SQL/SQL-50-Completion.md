[SQL 50 BADGE](image-1.png)


# SQL 50 — Completion Log
**Date Completed:** May 10, 2026
**Badge:** LeetCode SQL 50 ✓
**Duration:** ~2 weeks

---

## What SQL 50 Is
50 curated problems covering every core SQL concept needed for
data engineering and analytics interviews. Not random — structured
from basic SELECT to advanced window functions and CTEs.

---

## Topic Categories Covered

### 1. Basic SELECT & Filtering
Foundations — WHERE, LIKE, BETWEEN, NULL handling, DISTINCT.

**DE Connection:** Every pipeline query starts here. dbt models,
Glue scripts, Spark SQL — all build on clean filtering logic.
Garbage filter = garbage pipeline output.

---

### 2. Basic Joins (INNER, LEFT, RIGHT, SELF)
Combining tables on keys. Self-joins for hierarchical/comparative data.

**DE Connection:** Star schema queries in data warehouses (Redshift,
BigQuery, Snowflake) are almost entirely JOIN operations between
fact and dimension tables. Getting joins wrong = wrong metrics served
to dashboards.

---

### 3. Aggregations (GROUP BY, HAVING)
COUNT, SUM, AVG, MAX, MIN with GROUP BY. HAVING to filter
aggregated results.

**DE Connection:** Every business metric is an aggregation —
daily revenue, monthly active users, average order value.
In DE: these are the transformation layer queries in your pipeline
before data lands in the serving layer.

---

### 4. Sorting & Ranking (ORDER BY, LIMIT, OFFSET)
Result ordering, pagination, top-N retrieval.

**DE Connection:** Top-K queries appear constantly —
top products, top customers, top error types.
LIMIT + OFFSET is how paginated APIs serve data from SQL backends.

---

### 5. Subqueries & Nested Queries
Scalar subqueries, correlated subqueries, IN / NOT IN / EXISTS.

**DE Connection:** Data quality checks in pipelines use this pattern —
"find records that exist in table A but not in table B" =
NOT EXISTS / NOT IN. Used in deduplication and reconciliation jobs.

**Example from log:** LC 585 Insurance — composite filter using
subquery on (lat, lon) uniqueness before outer GROUP BY.

---

### 6. UNION & UNION ALL
Combining result sets vertically. UNION deduplicates, UNION ALL preserves.

**DE Connection:** Merging data from multiple sources into one
result set — combining sales from two regions, merging bidirectional
relationships (requester + accepter), consolidating logs from
multiple tables into one audit view.

**Example from log:** LC 602 Friend Requests — UNION ALL both
directions of friendship, then aggregate to get total per person.
LC 1341 Movie Rating — two independent ranked subqueries merged
into one output.

---

### 7. String Functions & Date Functions
SUBSTRING, CONCAT, LENGTH, DATE_FORMAT, DATEDIFF, YEAR, MONTH.

**DE Connection:** Raw data is messy — dates arrive as strings,
names need parsing, timestamps need truncation to day/month/year.
In DE: these are the cleaning transformations in your Bronze→Silver
layer of a Medallion Architecture pipeline.

---

### 8. Window Functions (RANK, DENSE_RANK, ROW_NUMBER, LAG, LEAD)
Partitioned ranking and offset functions without collapsing rows.

**DE Connection:** The most powerful SQL feature for analytics pipelines.
- RANK / DENSE_RANK → leaderboards, top-N per group
- LAG / LEAD → month-over-month comparisons, churn detection
- ROW_NUMBER → deduplication (keep latest record per user)

In DE: window functions are the core of dbt analytical models
served to BI tools. Knowing these deeply = knowing how
analysts actually consume pipeline output.

---

### 9. Rolling Aggregations (ROWS BETWEEN frame)
SUM/AVG over a sliding window of rows.

**DE Connection:** 7-day rolling revenue, 30-day moving average,
trailing metrics — every business dashboard has these.
In DE: this is what you build in Spark window functions or
dbt models before the data hits Tableau or Metabase.

**Example from log:** LC 1321 Restaurant Growth — 7-day rolling
SUM and AVG using ROWS BETWEEN 6 PRECEDING AND CURRENT ROW,
with subquery to collapse daily duplicates first.

---

### 10. CTEs (Common Table Expressions)
WITH clause for readable, modular query decomposition.

**DE Connection:** CTEs are how production SQL is written —
not nested subqueries, but named logical steps.
dbt models are essentially CTEs compiled into views/tables.
Every senior DE writes in CTEs. This is the professional standard.

**Example from log:** LC 602 — two CTEs to separate individual
counts from total aggregation before final filter.

---

## Patterns That Repeated

| Pattern | Problems It Solved |
|---|---|
| Subquery for filter then outer aggregate | Insurance, Department salaries |
| UNION ALL bidirectional + aggregate | Friend Requests, similar graph problems |
| Window fn + ROWS frame + subquery pre-agg | Restaurant Growth, moving averages |
| CTE decomposition for readability | Multiple medium/hard problems |
| DATE_FORMAT for month-level grouping | Movie Rating, date-filtered aggregations |

---

## Honest Reflection
Not every problem was logged in detail during the solve.
The problems documented with full approach + real-world connection:
- LC 1341 Movie Rating (UNION ALL + ranked subqueries)
- LC 1321 Restaurant Growth (rolling window + ROWS frame)
- LC 602 Friend Requests (bidirectional UNION ALL + CTE)
- LC 585 Insurance (composite subquery filter)

These four represent the hardest patterns in the set.
The remaining problems were solved but not individually logged —
this completion document is the honest summary of what was covered.

---

## What's Next
**Advanced SQL 50** — every problem gets a proper log entry.
No exceptions.

Topics incoming: recursive CTEs, complex window combinations,
query optimization, execution plans.