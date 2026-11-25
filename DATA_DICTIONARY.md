# Data Dictionary

All files are in `data/`. Dates are `YYYY-MM-DD`. The data runs to 2026-09-30.

## accounts.csv
One row per account (a company that is a customer or a prospect).

| Column | Description |
|--------|-------------|
| account_id | Account identifier |
| account_name | Company name |
| account_type | `Customer` or `Internal` |
| industry | Industry |
| billing_country | Billing country |
| region | Sales region: North America, EMEA or APAC |
| created_date | Date the account was created in the CRM |

## account_segment_history.csv
The customer segment (`SMB`, `Mid-Market`, `Enterprise`) of each account over
time. An account's segment can change.

| Column | Description |
|--------|-------------|
| account_id | Account identifier |
| segment | Segment during this period |
| valid_from | First day of the period |
| valid_to | First day of the next period (exclusive). Empty for the current segment. |

## products.csv

| Column | Description |
|--------|-------------|
| product_id | Product identifier |
| product_name | Product name |
| product_family | Platform, Monitoring, Developer Tools or Services |
| revenue_type | `recurring` (annual subscription) or `one_time` (fixed fee) |
| unit | What the quantity counts: license, domain, seat, engagement, session |

## subscription_lines.csv
One row per product on a contract.

| Column | Description |
|--------|-------------|
| line_id | Line identifier |
| contract_id | Contract the line belongs to |
| account_id | Account that bought it |
| product_id | Product |
| start_date | First day of service |
| end_date | Last day of service (inclusive) |
| quantity | Number of units |
| annual_unit_price | For recurring products, the price per unit per year. For one-time products, the fee per unit. In the line's currency. |
| discount_pct | Discount as a fraction (0.1 = 10%) |
| currency | Currency of the price |
| status | `active`, or `void` if the line was entered in error |
| renewal_of_line_id | For a renewal, the line it renews. Empty otherwise. |

## fx_rates.csv
Monthly exchange rates: one rate per currency per month.

| Column | Description |
|--------|-------------|
| rate_month | First day of the month |
| currency | Currency code |
| usd_per_unit | US dollars per one unit of the currency |

## Business definitions

- **ARR on a date** is the sum, over recurring lines in service on that date, of
  `quantity x annual_unit_price x (1 - discount_pct)`, converted to USD.
  One-time products are not ARR.
- **Currency conversion:** use the rate for the month in which the line starts,
  so a line's USD value does not change over its life.
- **Renewals:** when a renewal line starts, the line it renews stops counting.
- **Customers:** internal and test accounts are not customers and are excluded
  from all metrics.
- **NRR** for the 12 months ending on date D: take the accounts with ARR above
  zero 12 months before D. NRR = their total ARR on D divided by their total ARR
  12 months before D. **GRR** is the same, but each account's ARR on D is capped
  at its starting ARR (it counts churn and downgrades, not growth).
