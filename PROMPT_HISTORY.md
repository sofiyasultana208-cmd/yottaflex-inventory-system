# My AI Prompt History & Development Log

I used Gemini AI to help me plan, generate the data, build the dashboard, and troubleshoot errors for this YottaFlex project. 

Even though I used AI to speed things up, I personally checked all the Excel sheets, tested the ATP math formula, debugged local setup issues, and made sure the final Streamlit app worked cleanly.

---

## 1. Setting Up the System & Excel Sheets

**What I asked:**  
> "Act as a Forward Deployed Engineer at YottaFlex. I need to build an inventory system for 11 sheets: Products, SKUs, Locations, InventoryBalances, Orders, OrderLines, Reservations, InventoryMovements, Shipments, ReplenishmentRules, and GroundTruth. Give me the schema, primary keys, and foreign keys."

**What we did:**  
We picked consistent ID formats like `SKU-000001`, `LOC-000001`, and `ORD-2026-000001` so all 11 sheets link together properly without missing records.

---

## 2. Generating Data & Adding Stock Rules

**What I asked:**  
> "Write a Python script using Pandas to create data for all 11 tables. Make an append-only movement log for stock changes and calculate Available-to-Promise using: ATP = On-Hand - Reserved - Blocked + In-Transit."

> "Also, add some real-world errors into a separate GroundTruth sheet (like oversold items or broken stock) so we can test if the system notices them."

**What we did:**  
Generated the main `yottaflex_inventory_data.xlsx` workbook. It includes both normal store stock data and a separate list of labelled anomalies for testing.

---

## 3. Checking Data Quality

**What I asked:**  
> "Write a Python script (`validator.py`) to check that all IDs match, no primary keys are duplicated, and the stock math adds up correctly. Put the results in a `ValidationSummary` sheet."

**What we did:**  
Ran automated checks to confirm 100% foreign key matching and verified that the stock balances reconciled across all sheets.

---

## 4. Building the Web Dashboard (`app_yotta.py`)

**What I asked:**  
> "Write a dark-themed Streamlit app (`app_yotta.py`) with a sidebar menu, big metric cards, a search bar for SKUs, an ATP viewer, a movement log viewer, and a tab to show the GroundTruth errors and audit summary."

**What we did:**  
Created the frontend app layout so operations managers can view inventory metrics and search through data visually instead of scrolling through spreadsheets.

---

## 5. Fixing Errors & Local Setup Problems

**Issue 1: Jupyter cell magic & tunnel error in Colab**  
* *What I asked:* "I got `UsageError: Line magic %%writefile not found` and localtunnel failed in Colab. How do I fix this?"  
* *Fix:* Downloaded `app_yotta.py` and the Excel file directly to my computer and ran Streamlit locally using the terminal.

**Issue 2: Streamlit couldn't find the Excel file**  
* *What I asked:* "Streamlit says `CRITICAL ERROR: Could not find yottaflex_inventory_data.xlsx`. Why?"  
* *Fix:* My browser had renamed the file to `yottaflex_inventory_data (2).xlsx`. I renamed it back to `yottaflex_inventory_data.xlsx` in my project folder, and the app loaded instantly.

---

## 6. Host & Publish Live App

**What I asked:**  
> "How do I deploy this Streamlit app to Streamlit Community Cloud so anyone can click the link in my README to see the live app?"

**What we did:**  
Connected my public GitHub repository to Streamlit Community Cloud, set `app_yotta.py` as the main file, and generated a working public URL.

---

## What I Personally Verified & Tested
- **ID Matching:** Checked that parent catalog IDs (`SKU-000001`, `LOC-000001`) match up across child sheets like OrderLines and Movements.
- **ATP Math:** Tested edge cases to make sure negative ATP values get flagged correctly.
- **Dashboard UI:** Clicked through every view, tested search filters, and checked table layouts.
- **Public Link Check:** Opened the GitHub repo and live Streamlit link in a private/incognito browser window to make sure anyone can view them.