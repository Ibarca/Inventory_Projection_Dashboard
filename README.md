# Inventory Projection Dashboard (BigQuery SQL + Looker Studio)


## Overview

This project showcases a **production-ready inventory projection model** built in **BigQuery SQL** and consumed by **Looker Studio** for day-to-day Category Management and Supply Chain decision-making.

The model produces a **weekly SKU-level projection (ISO weeks / KW)** for 2026, combining historical demand, current stock, and inbound purchase orders into a single, scalable dataset. It reflects how inventory is actually planned and reviewed in data-driven e-commerce organizations.

---

## Why This Matters for the Business

Poor inventory visibility leads directly to:

* lost sales due to stockouts
* excess capital tied up in slow-moving stock
* reactive rather than planned purchasing decisions

This project addresses those risks by:

* making **stockout risk visible weeks in advance**
* translating raw data into **actionable KPIs** (reach, service level, risk)
* prioritizing SKUs using **ABC / Pareto logic**, not gut feeling
* aligning inventory decisions with **revenue impact**

For Category Managers, this enables proactive steering of availability, purchasing, and supplier discussions instead of firefighting.

---

## Core Logic (Category-Focused)

### Demand

Demand is estimated using a transparent **run-rate forecast**:

* 2025 sales are converted into daily velocity
* weekly demand = daily velocity × 7

This avoids black-box forecasting and keeps assumptions easy to explain to stakeholders.

### Inbound & Stock Projection

Inbound purchase orders are aggregated by **expected delivery ISO week**. Inventory is then projected week by week using:

> projected stock = max(0, previous stock + inbound − demand)

The **true zero floor** ensures realistic availability and prevents misleading negative stock values.

### Reach, Service Level & Risk

From the weekly projection, the model derives:

* **Reach in weeks** (how long stock lasts)
* **Projected service level** for the next 24 weeks
* **Stockout risk buckets** (Critical → No risk)
* **First projected stockout date**

These metrics are designed to be directly usable in weekly category reviews and replenishment planning.

### ABC Prioritization

SKUs are classified based on **2025 revenue contribution**:

* A: top 40% of revenue
* B: next 40%
* C: remaining 20%

This ensures that attention is focused where business impact is highest.

---

## Output Dataset

The final table is intentionally **denormalized and BI-ready**, with one row per SKU and ISO week.

Key fields include:

* SKU attributes (category, brand, supplier)
* Weekly projected stock and stock value
* Weekly inbound and demand
* Reach in weeks and stockout risk
* Projected service level (next 6 months)
* Revenue rank and ABC class

This structure keeps Looker Studio fast and avoids complex calculations in the BI layer.

---

## Dashboard Usage (Looker Studio)

The dataset feeds an interactive dashboard used for:

* daily inventory monitoring
* weekly category and supply reviews
* SKU-level prioritization
* identifying when and where action is required

Filters allow slicing by SKU, risk level, ABC class, category, brand, and supplier.

---

## How Results Can Be Validated

The model is designed to be easy to validate:

* **Week 1 stock** matches the inventory snapshot
* **Inbound quantities** reconcile with purchase orders by delivery week
* **Demand** can be traced back to historical sales volumes
* **Stock evolution** follows a simple, auditable formula
* **Service level** equals the share of weeks with stock > 0 in the forward window

Because all calculations run in SQL, every KPI can be recomputed, inspected, and explained end-to-end.

---

## Scalability & Reusability

* All heavy logic runs in **BigQuery SQL**
* Suitable for **thousands of SKUs**
* New KPIs (safety stock, lead-time buffers, forecast overrides) can be added without changing the dashboard structure

This approach has been applied and refined in real Category Management environments and is built to scale with the organization.

---

## Tech Stack

* BigQuery (advanced SQL)
* Looker Studio
* Recursive CTEs
* Window functions
* ISO calendar logic

---

## Disclaimer

All data used in this project is synthetic and created for portfolio purposes. The logic and structure reflect real-world production use cases in e-commerce and retail inventory management.
