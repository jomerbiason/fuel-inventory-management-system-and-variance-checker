# Enterprise Station Fuel IMS & Forecasting Dashboard

An industry-standard, single-file **Fuel Inventory Management System (IMS)**, **Financial Variance Auditor**, and **Underground Storage Tank (UST) Order Forecaster**. This system is specifically engineered to map onto real-world fuel retail environments—featuring localized support for Philippine Suggested Retail Price (SRP) cycles ("Tuesday Adjustments") and strict wet-stock discrepancy thresholds.

Built completely using modern vanilla web technologies (**HTML5**, **CSS3 Custom Properties**, and **ES6 JavaScript**) with `localStorage` persistence and full offline utility.

---

## 🚀 Live Features

* **⚡ Real-Time Tank Asset Monitor:** Visually tracks active volume capacities against safe operational levels with dynamic progression gauges.
* **⛽ Live SRP Board Price Configuration:** Allows immediate overriding of fuel rates to reconcile calculations accurately against the standard Philippine Tuesday morning market adjustments.
* **📊 Shift Reconciliation Engine:** Automates daily closing book audits by cross-referencing computer terminal logs with physical dipstick verifications.
* **⚠️ Smart Priority Forecasting:** Automatically alerts managers when fuel volumes fall below the standard **30% safety threshold** to prevent pump line debris clogging and operational dry-outs.
* **📈 Built-In Compliance Audit Ledger:** Generates instant flags for any volumetric variance exceeding **0.5%** of throughput capacity.
* **💾 Local Storage & CSV Exporting:** Features immediate caching across system reboots along with standard tabular data downloading (.CSV formatting) for external report routing.

---

## 🛠️ The Operational Context (Ph-SRP Framework)

This software framework matches the strict logistics workflow practiced across national service stations (e.g., Shell, Petron, Caltex, CleanFuel):

### 1. The Tuesday Price Adjustment Cycle
In the Philippines, oil terminal networks announce downstream market rate movements every Monday afternoon. These structured price shifts take legal effect on the pumps exactly at **6:00 AM on Tuesday**. This dashboard provides a targeted **SRP Board Configuration Panel** that lets operations managers load incoming values overnight, preserving book asset accuracy before morning shifts clock in.

### 2. Physical Wet Stock Discrepancy Auditing
Fuel is volatile; thermal shifts, tank sludging, and high-pressure nozzle deliveries cause natural shrinkage. By processing physical dip values against virtual ledger counts, the **Shift Reconciliation Input** catches variance leaks early and evaluates their direct monetary loss (₱) against active pump rates.

---

## 📂 File Structure & Tech Stack

The entire software solution is contained within an optimized, componentized architecture embedded inside a singular workspace file for trivial field deployment:

```bash
├── index.html     # Application Core (UI layout, Theme Engine, Calculation Script)
