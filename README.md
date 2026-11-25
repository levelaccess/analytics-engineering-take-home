# Analytics Engineering Take-Home

Thanks for taking the time to do this exercise. It should take **2 to 3 hours**.
If you reach 3 hours, stop and write down what you would do next. That counts.

## The scenario

Acme Accessibility sells accessibility software to other businesses on annual
subscriptions. Leadership wants a trusted view of **Annual Recurring Revenue
(ARR)** and **customer retention**. You have an export of the subscription data
in `data/`. Your job is to model it so analysts can answer these questions, and
to answer them yourself.

The data is small on purpose, so you can open it in a spreadsheet. It is a
realistic export and has not been cleaned for you.

Like real work, not everything is spelled out. Where something is unclear,
make a reasonable assumption, write it down, and keep going. There is no one to
ask, so we will not answer clarifying questions before the demo.

## What to do

**1. Design a dimensional model.**
Build a small star schema: fact and dimension tables that an analyst could use
without knowing the quirks of the raw data. For each table, state its **grain**
(what one row represents) and its keys.

**2. Build it and answer three questions.**

| # | Question |
|---|----------|
| Q1 | What was total ARR at each quarter-end: 2025-12-31, 2026-03-31, 2026-06-30 and 2026-09-30? Break the 2026-09-30 figure down by **region** and by **product family**. |
| Q2 | What were **Net Revenue Retention (NRR)** and **Gross Revenue Retention (GRR)** for the 12 months ending 2026-09-30, by customer **segment**? |
| Q3 | How many customers did Acme have on 2026-09-30? Finance counts accounts with ARR above zero. Customer Success counts any account with a product in service, including one-time services. Give both numbers and recommend which one leadership should use. |

Business definitions are in [DATA_DICTIONARY.md](DATA_DICTIONARY.md).

**3. Write a short note (one page is enough).**
- Your model: a diagram or a table list with the grain of each table.
- The data issues you found, and what you did about each one.
- Any assumptions you made where the rules were unclear.
- What you would change to run this in production.

## Tools

Use anything you are comfortable with: dbt, plain SQL, Python, Databricks,
Snowflake, BigQuery, Postgres. If you have no setup, DuckDB reads the CSVs
directly:

```bash
pip install duckdb
python -c "import duckdb; print(duckdb.sql(\"select * from 'data/accounts.csv' limit 5\"))"
```

**AI tools are welcome.** Tell us briefly where you used them. In the demo, you
will be asked to explain and change your work live, so make sure you understand
every decision in it.

## What to submit

Submit at least 24 hours before your demo:
- your code (SQL, dbt project, or notebook);
- your answers to Q1 to Q3 (a table or CSV is fine);
- your note.

Send it as a **private** GitHub repository shared with the reviewers named in
your invite email, or as a zip file. Please do not fork this repository
publicly or post your solution.

## The demo (45 minutes)

| Time | What happens |
|------|--------------|
| 5 min | Introductions |
| 15 min | You share your screen and walk us through your model, your answers and the data issues you found. No slides needed; show the real work. |
| 15 min | We ask questions about your decisions. |
| 10 min | We ask for a small change to your model and you make or describe it live, thinking out loud. You can use your usual tools, AI included. |

We are not looking for a perfect answer. We are looking for how you model data,
how carefully you check it, and how clearly you explain your choices.
