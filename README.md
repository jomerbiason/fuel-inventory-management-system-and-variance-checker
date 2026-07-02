# ⛽ Fuel Inventory Management System & Variance Checker

A high-performance, lightweight single-page application (SPA) built for retail fuel station operations in the Philippines. This system handles real-time wet stock reconciliation, Philippine Suggested Retail Price (Ph-SRP) financial auditing, automated Underground Storage Tank (UST) priority order forecasting, market price benchmarking, and nearby station discovery.

## 🚀 Live Demo

[**Access the Fuel Management Dashboard**](https://jomerbiason.github.io/fuel-inventory-management-system-and-variance-checker/)

## 🗺️ Local Market Context: "Tuesday Adjustments"

In the Philippine downstream oil industry, fuel pricing follows a structured routine:

1. **Monday Afternoon:** Oil firms announce nationwide price hikes or rollbacks.
2. **Tuesday Morning (6:00 AM):** These pricing updates officially go live.

This application is built directly into that operational workflow. Station managers configure the price matrix during the pre-dawn hours on Tuesday. Once saved, the transaction system instantly tracks variances and asset sheets against the true running pump rates for that shift cycle.

## 🛠️ Key System Features

* **Wet Stock Audit Engine:** Cross-examines computer sales against manual physical dipstick readings.
* **0.5% Industry Standard Safeguard:** Automatically flags inventory discrepancies as CRITICAL if they exceed the industry-standard 0.5% volumetric threshold.
* **Historical Price Lock:** Historic transactions retain their exact pricing metrics to protect financial auditing records from retrospective drift.
* **UST Forecasting:** Real-time progress bars provide visual alerts. If tanks drop to or below 30% capacity, the system triggers a Priority Order Alert.
* **Editable Price Matrix:** Manually configure the SRP board rate per product line (Diesel, 91 RON, 95 RON, 97 RON) at any time.
* **Market Reference Comparator:** Benchmark your board against indicative SRP figures for Petron, Shell, Caltex, or SeaOil, and one-click apply them into your own Price Matrix for review before saving. The snapshot's age is calculated live against today's date and flags itself as stale after a couple of months so it never masquerades as current data.
* **Nearest Fuel Station Locator:** Uses your device's location and live OpenStreetMap data to find real nearby stations, filterable by brand (Petron, Shell, Caltex, SeaOil, or all), sorted by distance, with an interactive map and one-tap turn-by-turn directions.
* **Audit Ledger Management:** Full transaction history with a running summary (entry count, critical-flag count, net variance volume/value) and per-entry deletion for correcting mistaken records.
* **Accessible by Design:** Keyboard-navigable controls, ARIA labeling on dynamic regions (tank gauges, live results, station search status), and respect for reduced-motion preferences.
* **Resilient Local Storage:** Corrupted or missing browser storage is detected and safely reset rather than crashing the app.
* **GitHub Pages Ready:** Fully optimized for static hosting — no backend, build step, or server required.

## 📐 Mathematical Blueprint

### Daily Book Inventory Balance

The expected book stock is calculated as:

```
I_expected = (I_opening + V_delivery) - V_sales
```

### Variance Monetary Evaluation

The financial impact is determined by:

```
E_monetary = (I_physical - I_expected) * P_SRP
```

*(Where `P_SRP` is the immutable board rate at the time of the transaction)*

### Critical Variance Threshold

A transaction is flagged **CRITICAL** when:

```
|I_physical - I_expected| > (V_sales * 0.005)
```

## 📡 Market Reference Comparator

Because there is no free, reliable, real-time public API for Philippine pump prices — and third-party trackers frequently disagree with each other by several pesos per liter — this feature intentionally does **not** claim to be a live feed. Instead:

* Reference figures are a manually-sourced, dated snapshot bundled into the app (`MARKET_REFERENCE` in the script).
* The UI computes and displays how many months old that snapshot is on every page load, escalating from a soft warning to an explicit "likely stale" notice over time.
* Applying a brand's reference prices only populates the Price Matrix input fields — nothing is saved until you explicitly click **Save Price Matrix**.
* Always cross-check against the [DOE's official Oil Monitor advisory](https://doe.gov.ph/oil-monitor) before relying on these figures operationally.
* To refresh the snapshot, edit `MARKET_REFERENCE.snapshotDate`, `asOfLabel`, and the per-brand price object directly in `index.html`.

## 🧭 Nearest Fuel Station Locator

* Requests the browser's Geolocation API for the user's current position (nothing is transmitted anywhere except the search query described below).
* Queries the free [Overpass API](https://overpass-api.de/) for OpenStreetMap `amenity=fuel` nodes within a configurable radius (3–20 km) — no API key or billing account required.
* Filters results by brand (matched against OSM `name`/`brand`/`operator` tags) and sorts by great-circle distance.
* Renders results as a distance-sorted list with "Directions" deep links to Google Maps, plus an interactive [Leaflet](https://leafletjs.com/) map.
* Station coverage depends on OpenStreetMap's community-maintained data — generally strong in Metro Manila and other major cities, sparser in some rural areas.
* Requires an internet connection to reach the map tiles and Overpass API (the core inventory/audit features work fully offline once loaded).

## 🚀 How to Run Locally

Because this application is a pure client-side SPA, you can run it directly in your browser without any backend dependencies:

1. **Clone the repository:**
   ```
   git clone https://github.com/jomerbiason/fuel-inventory-management-system-and-variance-checker.git
   ```
2. **Open the project:**
   Simply open `index.html` in your favorite web browser (Chrome, Edge, or Firefox).
3. **Deploying to GitHub Pages:**
   If you make changes, simply push your code to the `main` branch. GitHub Actions will automatically redeploy your updates to your live link.

> **Note:** The Market Reference Comparator and Nearest Station Locator load Leaflet from `cdnjs.cloudflare.com` and query `overpass-api.de`, so those two features require an active internet connection even when the app is otherwise running fully offline.

## 📋 Data Persistence

This system uses browser `localStorage`. Your data is private and saved locally on your machine — nothing is transmitted to a server. You can export your audit logs at any time using the "Export Audit Sheet (.CSV)" button within the application, or wipe the local cache with "Wipe Data Cache" to reset to defaults.

## 🧱 Tech Stack

* Vanilla HTML5 / CSS3 (custom properties for theming, light/dark mode) / JavaScript (ES6+) — zero build step, zero framework dependencies.
* [Leaflet](https://leafletjs.com/) (via CDN) for interactive maps.
* [OpenStreetMap Overpass API](https://overpass-api.de/) for live fuel station data.
* Browser `localStorage` and Geolocation APIs.

## ⚖️ License

Distributed under the MIT License.
