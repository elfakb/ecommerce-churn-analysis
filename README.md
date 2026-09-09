# Customer Churn Reduction Analysis
### End-to-End Business Analysis Case Study | Olist Brazilian E-Commerce Dataset

---

## Project Overview

This project is a full-cycle business analysis case study built on the publicly available
**Olist Brazilian E-Commerce Dataset (Kaggle)**. It covers the complete BA workflow:
stakeholder interviews → requirements documentation → SQL analysis →
Excel dashboard → Agile sprint management → data-driven recommendations.

> **Scope note:** Classic churn (no repeat purchase) is not meaningful here — 96.9% of
> customers ordered only once. The scope was reframed to **customer dissatisfaction and
> brand trust risk**, a common real-world scope-clarification outcome.

---

## Dataset

| Detail | Value |
|---|---|
| Source | [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) |
| Period | Sep 2016 – Aug 2018 |
| Delivered orders | 96,353 |
| Tables used | orders, customers, order_reviews, order_payments, order_items, products, category_name_translation |

---

## Key Findings

| Finding | Detail |
|---|---|
| Late delivery impact | Avg review score drops from **4.29 → 2.57** when delivery is late |
| Peak dissatisfaction | **21.2%** in March 2018 (vs ~10% baseline) |
| Worst categories | office_furniture (21.9%), audio (21.6%), home_confort (18.1%) |
| Worst states | AL (21.4%), MA (19.8%), SE (18.9%) |
| Voucher effect | Voucher users repurchase at **10.1%** vs 6.4% for credit card |


---

## Dashboard Screenshots

### Executive Summary
![Executive Summary](screenshots/01_executive_summary.png)

### Monthly Dissatisfaction & Late Delivery Trend
![Monthly Trend](screenshots/02_monthly_trend.png)

### Category Breakdown
![Category Breakdown](screenshots/03_category_breakdown.png)

### State Breakdown
![State Breakdown](screenshots/04_state_breakdown.png)

### Payment Type Analysis
![Payment Type](screenshots/05_payment_type.png)

---

## SQL Highlights

**Late delivery vs. satisfaction:**
```sql
SELECT
    CASE WHEN julianday(order_delivered_customer_date) >
              julianday(order_estimated_delivery_date)
         THEN 'Late' ELSE 'On Time' END AS delivery_status,
    AVG(review_score) AS avg_score,
    COUNT(*) AS order_count
FROM orders o
LEFT JOIN order_reviews r ON o.order_id = r.order_id
WHERE o.order_status = 'delivered'
GROUP BY delivery_status;
```

---

## Agile Process

The project was managed across **3 × 2-week Sprints**:

- **Sprint 1** — Stakeholder interviews, requirements doc, data cleaning & loading
- **Sprint 2** — SQL analysis, hypothesis testing, breakdown queries
- **Sprint 3** — Excel dashboard, executive presentation

Key retrospective insight: the original churn hypothesis was invalidated by the data in Sprint 1,
and the scope was reframed collaboratively with the business sponsor — a real-world example
of Agile's "inspect and adapt" principle.

---

## Recommendations

1. **Tighten SLAs** with logistics partners, especially in AL, MA, SE, RJ
2. **Raise packaging standards** for furniture, audio, and large-volume categories
3. **Add structured complaint fields** to the review form (delay / damage / wrong item / other)
4. **Scale voucher campaigns** — voucher users repurchase at 1.6× the rate of credit card users

---

## Tools Used

![SQL](https://img.shields.io/badge/SQL-SQLite-blue)
![Excel](https://img.shields.io/badge/Excel-Dashboard-green)
![Agile](https://img.shields.io/badge/Method-Agile%20Scrum-orange)

---

## About

Business Analyst portfolio project. All numerical findings are from real public data.
Company name, stakeholder names, and meeting notes are fictional for demonstration purposes.
