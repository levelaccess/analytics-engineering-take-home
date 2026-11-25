# Analytics Engineering Take-Home

Thanks for doing this exercise. It should take no more than 1.5 to 2 hours.

## Scenario

Acme Accessibility sells accessibility software to businesses on annual
subscriptions. Leadership wants to track Annual Recurring Revenue (ARR) and
customer retention. The `data/` folder has an export of the subscription data.
Model it so an analyst can answer the questions below, then answer them.

The data is small, so you can open it in a spreadsheet. It has not been
cleaned.

Not everything is spelled out. Where something is unclear, make an assumption,
write it down and carry on. We won't answer questions about the exercise
before the demo.

## Tasks

1. Design a star schema. For each table, give its grain (what one row
   represents) and its keys.

2. Build it and answer these questions:

   - Q1. What was total ARR on 2025-12-31, 2026-03-31, 2026-06-30 and
     2026-09-30? Break down the 2026-09-30 figure by region and by product
     family.
   - Q2. What were Net Revenue Retention (NRR) and Gross Revenue Retention
     (GRR) for the 12 months ending 2026-09-30, by customer segment?
   - Q3. How many customers did Acme have on 2026-09-30? Finance counts
     accounts with ARR above zero. Customer Success counts any account with a
     product in service, including one-time services. Give both numbers and
     say which one you would use.

   Column descriptions and business definitions are in
   [DATA_DICTIONARY.md](DATA_DICTIONARY.md).

3. Write a short note, one page at most, covering:
   - your model (a diagram or a list of tables with their grain)
   - data issues you found and how you handled them
   - assumptions you made
   - what you would change to run this in production

## Tools

Use whatever you like: dbt, SQL, Python, Databricks, Snowflake, BigQuery,
Postgres. If you don't have a database set up, DuckDB can query the CSV files
directly:

```bash
pip install duckdb
python -c "import duckdb; print(duckdb.sql(\"select * from 'data/accounts.csv' limit 5\"))"
```

You can use AI tools. Mention where you used them. In the demo we will ask you
to explain your work and make a change to it.

## Submission

Send the following at least 24 hours before your demo:

- your code (SQL, dbt project or notebook)
- your answers to Q1 to Q3
- your note

Share it as a private GitHub repository with the reviewers listed in your
invite email, or send a zip file. Please don't fork this repository publicly
or post your solution online.

## Demo (45 minutes)

| Time | Agenda |
|------|--------|
| 5 min | Introductions |
| 15 min | You share your screen and walk us through your model, answers and the data issues you found. No slides. |
| 15 min | Questions about your decisions |
| 10 min | We ask for a small change, and you make or describe it while talking it through. You can use any tools you normally use. |

We are most interested in how you model the data, how you check it, and how
you explain your decisions.
