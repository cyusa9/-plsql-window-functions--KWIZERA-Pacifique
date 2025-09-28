# -plsql-window-functions--KWIZERA-Pacifique

## Business Scenario Definition

### Business Context

**Rwanda Stock Exchange Trading Platform** - A digital investment platform serving Rwandan investors trading local stocks including Bank of Kigali (BK), MTN Rwandacell (MTNR), Bralirwa (BLR), I&M Bank (IMB), and Crystal Ventures (CML).

### Data Challenge

The platform needs to provide investors and analysts with comprehensive trading insights including:

- Performance rankings of stocks and investors
- Portfolio trend analysis and growth tracking
- Trading pattern identification
- Customer segmentation for targeted services

### Expected Outcome

Data-driven insights to help investors make informed decisions, optimize platform services, and identify market trends for strategic planning.

## Success Criteria (5 Window Functions)

### 1. Top Performing Stocks/Investors → RANK()

**Goal:** Identify top 5 stocks by trading volume and top 5 investors by portfolio value

**Window Function:** `RANK() OVER (ORDER BY total_value DESC)`

**Business Value:** Highlight market leaders and VIP customers

### 2. Running Transaction Totals → SUM() OVER()

**Goal:** Calculate cumulative trading volume and value over time

**Window Function:** `SUM(amount) OVER (ORDER BY transaction_date)`

**Business Value:** Track market activity trends and platform growth

### 3. Month-over-Month Performance → LAG()/LEAD()

**Goal:** Calculate monthly portfolio growth rates and stock price movements

**Window Function:** `LAG(monthly_value) OVER (PARTITION BY user_id ORDER BY month)`

**Business Value:** Identify investment performance patterns

### 4. Investor Segmentation → NTILE(4)

**Goal:** Segment users into quartiles based on portfolio value (Bronze, Silver, Gold, Platinum)

**Window Function:** `NTILE(4) OVER (ORDER BY portfolio_value)`

**Business Value:** Enable tier-based customer service and features

### 5. Moving Averages → AVG() OVER()

**Goal:** 3-month moving averages of stock prices and trading volumes

**Window Function:** `AVG(price) OVER (ORDER BY date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)`

**Business Value:** Smooth out price volatility for trend analysis

## Database Schema Summary

### Tables Overview

| Table | Purpose | Key Columns | Sample Data |
| --- | --- | --- | --- |
| **Users** | Investor profiles | UserID (PK), Username, Email, JoinDate | 101, KAYITARE_J, [kayitare.j@email.com](mailto:kayitare.j@email.com) |
| **Stocks** | Stock catalog | StockID (PK), Symbol, CompanyName | 1, BK, Bank of Kigali |
| **Transactions** | Trading records | TransactionID (PK), UserID (FK), StockID (FK), Type, Quantity, Price, Date | 1001, 101, 1, Buy, 50, 280.00 |
| **Holdings** | Current positions | UserID (FK), StockID (FK), QuantityOwned | 101, 1, 30 |

### ER Diagram Notes

![image.png](attachment:269387fc-5977-40d0-8abc-aa618ac20451:image.png)

## Implementation Plan

### Phase 1: Ranking Functions

```sql
-- Query 1: Top 5 stocks by total trading volume
-- Query 2: Top 5 investors by portfolio value
-- Query 3: Ranking users by number of transactions
```

### Phase 2: Aggregate Functions

```sql
-- Query 4: Running total of daily trading volume
-- Query 5: Cumulative portfolio values over time
-- Query 6: Compare ROWS vs RANGE window frames
```

### Phase 3: Navigation Functions

```sql
-- Query 7: Month-over-month portfolio growth
-- Query 8: Stock price change analysis
-- Query 9: Trading frequency trends
```

### Phase 4: Distribution Functions

```sql
-- Query 10: Customer tier segmentation (NTILE)
-- Query 11: Percentile rankings (PERCENT_RANK)
-- Query 12: Cumulative distribution (CUME_DIST)
```

### Insights

- Start with clean, well-partitioned datasets. For time series analytics, ensure each stock has a continuous date series. Fill missing trading days with 0 volume and last‑known price to avoid biased moving averages.
- Prefer PARTITION BY for per‑entity analytics. For example, compute moving averages per stock and MoM growth per user portfolio.
- Choose the right window frame. For price trends use ROWS BETWEEN 2 PRECEDING AND CURRENT ROW for true 3‑row moving windows. Use RANGE only when your ORDER BY keys are numeric or date values without duplicates that would widen frames unexpectedly.
- Ranking ties: RANK vs DENSE_RANK. Use DENSE_RANK when you want exactly 5 winners even with ties. Use RANK when ties should reserve positions.
- Performance tips: Pre‑aggregate large fact tables by day and stock before windowing. Add composite indexes on (stock_id, date) and (user_id, date) to accelerate ORDER BY and PARTITION BY.
- Investor tiers: NTILE is a good start. Consider business‑aligned cutoffs later (e.g., fixed thresholds or risk‑adjusted value) once you have distributions.
- MoM interpretations: Use LAG on month‑end snapshots, not raw transactions, to avoid double counting. Normalize by cash inflows to separate alpha from deposits.
- Anomaly detection: Compare current volume to a rolling AVG plus N standard deviations to flag unusual trading.

### Example Queries

```sql
-- Top 5 stocks by total trading volume (shares)
SELECT symbol,
       SUM(quantity) AS total_volume,
       RANK() OVER (ORDER BY SUM(quantity) DESC) AS rnk
FROM   transactions t
JOIN   stocks s ON s.stockid = t.stockid
GROUP  BY symbol
QUALIFY rnk <= 5; -- if QUALIFY unsupported, wrap as subquery
```

```sql
-- Investor monthly portfolio value snapshots and MoM change
WITH monthly AS (
  SELECT user_id,
         TRUNC(date, 'MM') AS month,
         SUM(quantity * price) AS month_value
  FROM   transactions
  GROUP  BY user_id, TRUNC(date, 'MM')
)
SELECT user_id,
       month,
       month_value,
       LAG(month_value) OVER (PARTITION BY user_id ORDER BY month) AS prev_value,
       ROUND( (month_value - LAG(month_value) OVER (PARTITION BY user_id ORDER BY month))
              / NULLIF(LAG(month_value) OVER (PARTITION BY user_id ORDER BY month), 0) * 100, 2) AS mom_pct
FROM   monthly;
```

```sql
-- 3-month moving average price per stock (row-based)
SELECT symbol,
       date,
       price,
       AVG(price) OVER (
         PARTITION BY stockid
         ORDER BY date
         ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS ma_3
FROM   prices p
JOIN   stocks s ON s.stockid = p.stockid;
```

```sql
-- Segment users into quartiles by portfolio value (snapshot table: portfolio_daily)
SELECT user_id,
       snapshot_date,
       portfolio_value,
       NTILE(4) OVER (ORDER BY portfolio_value) AS quartile
FROM   portfolio_daily
WHERE  snapshot_date = TRUNC(SYSDATE);
```

```sql
-- Rolling volume anomaly flag (mean + 2 stdev over last 20 days)
SELECT stockid,
       date,
       volume,
       AVG(volume) OVER (PARTITION BY stockid ORDER BY date ROWS BETWEEN 19 PRECEDING AND CURRENT ROW) AS avg20,
       STDDEV(volume) OVER (PARTITION BY stockid ORDER BY date ROWS BETWEEN 19 PRECEDING AND CURRENT ROW) AS sd20,
       CASE WHEN volume > avg20 + 2*sd20 THEN 1 ELSE 0 END AS is_anomalous
FROM   prices;
```

### Data Quality Checks

- Primary keys: ensure Transactions.TransactionID is unique. No duplicate trades.
- Referential integrity: all Transactions.UserID and StockID exist in Users and Stocks.
- Time consistency: trade Date not in the future. Prices aligned to exchange trading days.
- Negative or zero values: Quantity > 0 and Price > 0 for buys and sells.
- Snapshots: portfolio snapshots should be post‑close and consistent day to day.

### References

- Oracle Analytics: Analytic and Window Functions Overview — https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Analytic-Functions.html
- Windowing clauses (ROWS, RANGE) — https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/analytic-function.html#GUID-9C45C9D7-DC3B-49C8-8E7F-6E3A3E2F2F41
- LAG, LEAD — https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/LAG.html and https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/LEAD.html
- RANK, DENSE_RANK — https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/RANK.html and https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/DENSE_RANK.html
- NTILE — https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/NTILE.html
- AVG, SUM analytic — https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/AVG-Analytic.html and https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/SUM-Analytic.html
- YouTube tutorial: https://www.youtube.com/watch?v=Ww71knvhQ-s

