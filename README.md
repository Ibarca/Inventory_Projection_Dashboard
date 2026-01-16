# Inventory Projection Dashboard – BigQuery SQL

This repository contains a **production-ready BigQuery SQL query** that powers an end-to-end **Inventory Projection Dashboard**. The query consolidates sales history, inventory snapshots, incoming purchase orders, and calendar logic into a single analytical dataset used for **inventory risk monitoring, service-level projection, and stock prioritization**.

The dashboard is designed for **Category Management, Supply Chain, and Operations teams** and supports weekly, SKU-level decision making at scale.

---

## 📌 What this project does

The query generates a **weekly ISO-calendar inventory projection** per SKU, applying a **true stock floor (never below zero)** and enriching the results with:

• Projected inventory units and value over time
• Incoming inventory visibility and valuation
• Demand projections based on historical velocity
• Projected service level over a forward-looking horizon
• First expected stockout date and reach in weeks
• ABC classification based on revenue contribution
• Stockout risk and sales velocity segmentation

The output is consumed directly by a BI layer (for example Looker Studio or Google Sheets) to render the dashboard shown above.

---

## 🧠 Business use cases

• Identify SKUs at risk of stockout weeks in advance
• Prioritize replenishment decisions using ABC logic
• Monitor projected service levels at SKU and category level
• Evaluate the impact of incoming purchase orders on future availability
• Track inventory value evolution over time
• Segment assortment by sales velocity and risk

This logic has been implemented and refined in real business environments and is designed to handle **thousands of SKUs efficiently**.

---

## 🏗️ Data sources

The query integrates the following source tables:

• SKU master data (cost, brand, supplier, category)
• Daily sales history (used to compute annual demand and velocity)
• Inventory snapshot at the start of the projection horizon
• Incoming purchase orders with expected del
