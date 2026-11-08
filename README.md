# ⚡ YottaFlex Forward Deployed Engineering Assessment

> **🔗 Live Dashboard Demo:** [View YottaFlex Inventory & ATP System](https://yottaflex-inventory-system-cy6rqzz37bltxmu3vqj42b.streamlit.app/)

---

## 📌 Project Overview
This project implements an **Enterprise Inventory Unification System & Available-to-Promise (ATP) Engine** built for YottaFlex. It models complex, multi-echelon retail supply chain operations, handling immutable transaction event streams, inventory locks, real-time stock reservations, automated edge-case anomaly injection, and programmatic data validation gates.

---

## 🏗️ System Architecture & Workflow

The system is engineered as an end-to-end data pipeline adhering to strict enterprise standards:

1. **Master Data Generation:** Generates scale-tested master data across products, variant SKUs (with zero-padded formatting), and multi-region fulfillment locations.
2. **Opening Balances & Immutable Ledger:** Seeds initial inventory positions and processes millions of transaction events via an append-only, immutable movement ledger.
3. **ATP Calculation Engine:** Programmatically computes real-time stock availability using the core formula:
   $$\text{ATP} = \text{On-Hand} - \text{Reserved} - \text{Blocked} + \text{In-Transit}$$
4. **Automated Validation & Reconciliation Gate:** Audits relational integrity (Primary Keys & Foreign Keys) and financial inventory math across tables, outputting a consolidated validation report.
5. **Interactive UI/UX Dashboard (`app_yotta.py`):** Built using Streamlit to provide operations and business teams with executive visibility, deep search capabilities, and transparent exception tracking.

---

## 📊 Excel Data Model & Sheet Breakdown

The backend data workbook (`yottaflex_inventory_data.xlsx`) comprises **11 core entities** and an automated audit summary:

| Sheet / Entity Name | Description & Business Purpose |
| :--- | :--- |
| **Products** | Parent product catalog defining category-level attributes, brands, and base descriptions. |
| **SKUs** | Specific variant-level stock keeping units (tracked by size, color, and unique zero-padded IDs like `SKU-000001`). |
| **Locations** | Warehouses, fulfillment centers, and physical retail store hubs. |
| **InventoryBalances** | Current snapshot matrix storing real-time On-Hand, Reserved, Blocked, In-Transit, and calculated ATP stock levels per SKU and location. |
| **Orders** | Customer purchase order header records tracking order status, timestamps, and customer metadata. |
| **OrderLines** | Granular line items associated with customer orders, linking specific SKUs, requested quantities, and fulfillment statuses. |
| **Reservations** | Temporary inventory holds created during online checkouts or cart locks, complete with expiration tracking. |
| **InventoryMovements** | Immutable, append-only event ledger capturing every stock transition (Receipts, Sales, Returns, Transfers, Adjustments) with unique event IDs. |
| **Shipments** | Outbound logistics delivery tracking linked to customer orders and carrier dispatch milestones. |
| **ReplenishmentRules** | Automated restocking triggers and safety stock thresholds used to maintain optimal inventory levels. |
| **GroundTruth** | Labelled edge-case operational anomalies and intentional exceptions (e.g., oversold stock, unreleased expired reservations) injected for system stress-testing. |
| **ValidationSummary** | Automated reconciliation audit sheet detailing primary key uniqueness, foreign key consistency, and stock arithmetic checks. |

---

## 🚀 Key Engineering & Design Highlights
- **Immutable Ledger Pattern:** Modeled inventory movements as an append-only event log to ensure total auditability (similar to double-entry bookkeeping).
- **Programmatic ATP Engine:** Automated stock calculations preventing overselling by dynamically factoring in active reservations and in-transit shipments.
- **Automated Data Quality Gate:** Built programmatic checks verifying foreign key integrity across relational tables and validating inventory stock balance arithmetic.
- **Resilience Testing:** Injected 57+ targeted operational anomalies into a dedicated ground-truth layer to validate system exception handling.

- - **Development Methodology:** Built iteratively using structured prompt workflows, transitioning from modular backend data scripts in Google Colab to a fully packaged, enterprise-grade Streamlit deployment.
  - 
## 🛠️ Local Installation & Running Instructions

To run the dashboard locally on your machine:

1. Clone the repository and navigate to the project folder:
   ```bash
   git clone [https://github.com/your-username/yottaflex-inventory-system.git](https://github.com/your-username/yottaflex-inventory-system.git)
   cd yottaflex-inventory-system
