# Olist E-commerce Analytics

A portfolio project using SQL, Python, and dashboards to analyze marketplace sales, customer behaviour, delivery performance, and seller and product performance.

**Status:** Project setup. Data auditing, KPI calculations, and findings are pending.

## Project scope

The source of truth is **Olist Ecommerce Goals.pdf**, supplied in the project reference materials. The four analysis areas and 16 KPI definitions below follow its KPI registry. No results are claimed at this stage.

| Analysis area | Business questions |
| --- | --- |
| A. Sales performance | How have sales and order volumes changed over time? Which categories contribute most to sales? Are sales concentrated in particular regions? |
| B. Customer behaviour | How many customers make repeat purchases? How long do they take to purchase again? Which groups contribute most sales? |
| C. Delivery performance | How frequently are deliveries late? Which sellers or regions experience the longest delays? Are longer delivery times associated with lower review scores? |
| D. Seller and product performance | Which sellers and categories generate the most sales? Do high-volume sellers also deliver reliable service? |

## KPI registry

| # | Area | KPI | Definition from the source |
| --- | --- | --- | --- |
| 1 | Sales | Merchandise sales value | Sum of qualifying item prices |
| 2 | Sales | Order count | Number of distinct qualifying orders |
| 3 | Sales | Average order value (AOV) | Merchandise sales / qualifying orders |
| 4 | Sales | Monthly sales growth | Percentage change in monthly sales |
| 5 | Customers | Unique customers | Distinct customer_unique_id |
| 6 | Customers | Repeat purchase rate | Percentage of customers with 2+ qualifying orders |
| 7 | Customers | Purchase frequency | Qualifying orders / unique customers |
| 8 | Customers | Cohort retention rate | Percentage of a customer cohort purchasing again in a subsequent period |
| 9 | Delivery | Average delivery time | Mean days between purchase and actual delivery |
| 10 | Delivery | Late delivery rate | Percentage of delivered orders arriving after the estimated date |
| 11 | Delivery | Average delivery delay | Mean days late among late orders |
| 12 | Delivery | Average review score | Average customer rating (1-5) |
| 13 | Sellers & Products | Seller sales value | Merchandise sales grouped by seller |
| 14 | Sellers & Products | Seller order volume | Distinct orders associated with each seller |
| 15 | Sellers & Products | Seller average review score | Average associated order review score, subject to attribution limitations |
| 16 | Sellers & Products | Seller delivery reliability | Delivery performance associated with each seller, with multi-seller orders handled explicitly |

Before implementation, document qualifying order statuses, observation windows, cohort periods, missing-value handling, and seller attribution rules. The source does not fully specify these choices; they remain pending.

## Data and validation

The planned model covers nine tables: customers, orders, products, sellers, order_items, order_payments, order_reviews, geolocation, and product_category_translation. The source also uses product_category_name_translation for the translation table; reconcile this name during ingestion.

- Preserve raw tables unchanged. Record anomalies and whether affected records are retained, excluded, corrected, or flagged.
- Audit completeness, uniqueness, validity, referential integrity, consistency, and granularity.
- Use customer_unique_id for repeat purchasing; customer_id identifies customer records.
- Validate order keys, nonnegative prices and freight, payment values, timestamp chronology, review scores, and category and seller references.
- Handle missing delivery dates according to order status; a cancelled order without a delivery date is not automatically an error.
- Prevent duplicated sales when joining items, payments, and reviews.
- Resolve multiple reviews per order and explicitly document limitations for attributing order-level reviews and deliveries to sellers on multi-seller orders.
- Treat geolocation as multiple records per postal-code prefix, not a unique-key lookup.

Dataset acquisition, provenance, usage terms, date coverage, and environment setup will be documented before analysis. Raw datasets and secrets are excluded from version control.

## Repository structure

| Folder | Purpose |
| --- | --- |
| docs/ | Scope, KPI decisions, data dictionary, quality audit, and progress checklist |
| sql/ | Data validation, transformation, and KPI queries |
| python/ | Reproducible preparation and exploratory analysis |
| dashboards/ | Dashboard files, screenshots, and documentation |
| reports/ | Findings, limitations, and recommendations |

## Progress

See [the project checklist](docs/progress-checklist.md). Planned deliverables are validated SQL queries, reproducible Python analysis, dashboards covering the agreed areas, and a report connecting findings to business decisions.

## Working approach

Work in small, reviewable changes. Use a branch for each analysis task and a pull request to explain the business question, approach, validation, and limitations. Confirm KPI totals and join behaviour before publishing dashboard findings.
