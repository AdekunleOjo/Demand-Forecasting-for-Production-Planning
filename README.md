# Seasonal Demand Forecasting for Production Planning

A simple, Excel-based seasonal forecasting project that uses three years of monthly sales history to estimate month-by-month demand for 2026, so production can be planned around busy and quiet periods.

![demand-forecasting-production-planning](https://github.com/AdekunleOjo/demand-forecasting-production-planning/blob/main/forecast_chart.png)

## Problem

Demand is not flat across the year: some months sell far more than others. A production plan that assumes the same output every month will cause overproduction in slow months and shortages in peak months. The goal is to turn historical monthly sales into a **monthly demand forecast for 2026** that a production planner can use.

## Data

| File | Description |
|---|---|
| `Actual_Demand.xlsx` | Project brief: actual monthly demand (units) for three years |
| `Demand_Forecasting.xlsx` | Solution. `Sheet1` holds the calculations, `Sheet2` documents the method step by step |

Annual totals of the historical data: **930 → 1,053 → 1,155 units** (2023, 2024, 2025).

## Method: Seasonal Index

1. **Average demand by month.** For each month, average its demand across the three years (e.g. Jan = (61 + 103 + 131) / 3 = 98.3).
2. **Average monthly demand.** The average across all 36 data points (= 87.17 units).
3. **Seasonal index** = (average demand for the month) / (average monthly demand).
   - `1.0` = a normal month
   - `> 1` = above-average demand
   - `< 1` = below-average demand
4. **Forecast total for 2026.** Assumed demand is increasing, so 2026 total demand is set to **1,350 units**.
5. **Monthly forecast** = (1,350 / 12) × seasonal index.

In Excel (row 4 shown, filled down for all months):

```
F4: =AVERAGE(C4:E4)              Avg demand by month
G4: =AVERAGE($C$4:$E$15)         Avg monthly demand
H4: =F4/G4                       Seasonal index
I4: =($I$17/12)*H4               2026 monthly forecast
```

## Results

| Month | Avg Demand | Seasonal Index | 2026 Forecast (units) |
|---|---:|---:|---:|
| Jan | 98.3 | 1.13 | 127 |
| Feb | 105.0 | 1.20 | 136 |
| Mar | 42.0 | 0.48 | 54 |
| Apr | 111.7 | 1.28 | 144 |
| May | 44.0 | 0.50 | 57 |
| Jun | 62.3 | 0.72 | 80 |
| Jul | 127.7 | 1.46 | 165 |
| Aug | 96.3 | 1.11 | 124 |
| Sep | 77.0 | 0.88 | 99 |
| Oct | 57.3 | 0.66 | 74 |
| Nov | 85.7 | 0.98 | 111 |
| Dec | 138.7 | 1.59 | 179 |
| **Total** | | | **1,350** |

### Key takeaways

- **Peak months:** December (1.59), July (1.46) and April (1.28). Production capacity and inventory build-up should be prioritised ahead of these.
- **Low months:** March (0.48), May (0.50) and October (0.66). These are good windows for maintenance, reduced shifts or lower stock holding.
- Demand is clearly uneven: December's forecast is more than 3× March's.

## Assumptions and limitations

- **The 2026 total (1,350) is an assumption**, not a model output. Historical totals grew ~13% then ~10% year over year; 1,350 implies ~17% growth, which is more optimistic than the recent trend.
- Only **three observations per month**, so seasonal indices are sensitive to one unusual year (e.g. Sep 2025 jumped to 112 from 54 the year before).
- The method assumes the **seasonal pattern repeats** and that growth is spread proportionally across months.

## Tools

Microsoft Excel (`AVERAGE`, absolute references, fill-down formulas)

## Repository structure

```
.
├── README.md
├── forecast_chart.png
├── Actual_Demand.xlsx
└── Demand_Forecasting.xlsx
```
