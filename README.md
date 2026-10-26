# POS Manufacturing Analytics | Power BI Portfolio Project

**Sales performance, order fulfillment, and data quality analysis for a simulated point-of-sale (POS) manufacturing business.**

![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?logo=powerbi&logoColor=black) ![Power Query](https://img.shields.io/badge/Power%20Query-ETL-247A6B) ![DAX](https://img.shields.io/badge/DAX-Measures-327EC1) ![Data](https://img.shields.io/badge/Data-Synthetic-64748B)

## 📊 View the report

**[📄 View the report (PDF)](./POS_Manufacturing_Analytics.pdf)**  
**[⬇️ Download the interactive Power BI project (.pbix)](./powerbi/POS_Manufacturing_Analytics.pbix)**

The report is distributed as a **static PDF export** because a public Power BI Service link is not currently available. The PDF preserves the report pages and visuals, but **slicers, tooltips, drillthrough, and other interactive Power BI features cannot be used in the PDF**.

> **Repository setup:** Place `POS_Manufacturing_Analytics.pdf` in the repository root and `POS_Manufacturing_Analytics.pbix` in the `powerbi/` directory. The `.pbix` file can be downloaded and opened in Power BI Desktop to explore slicers, filters, the data model, Power Query transformations, and DAX measures.

## Project overview

This end-to-end business intelligence project simulates a manufacturing company producing point-of-sale displays and promotional materials. Its goal is to turn imperfect operational sales data into a reliable, decision-ready reporting model.

The workflow covers:

- Data profiling, cleaning, and validation in **Power Query (M)**.
- A relational **star-schema-style semantic model** with a sales fact table and supporting dimensions.
- Business metrics and filter-aware calculations using **DAX**.
- Interactive report design in **Power BI Desktop**.
- A separate **data quality audit** to preserve visibility into problematic source records.

All business data is **synthetic** and is not representative of a real company's performance.

## Report pages

| Page | Purpose |
| --- | --- |
| **01 · Executive Overview** | High-level order value, order volumes, completion rate, monthly trends, and order status breakdown. |
| **02 · Data Quality & Exceptions** | Audit findings, issue categories, pending reviews, and data quality trends. |
| **03 · Sales & Product Analysis** | Product contribution, regional results, salesperson performance, and customer analysis. |
| **04 · Order Details** | Order-level register, filters, financial values, and data quality indicators. |

The downloadable [Power BI Desktop project](./powerbi/POS_Manufacturing_Analytics.pbix) supports interactions such as slicers and contextual filtering; these are not available in the PDF export.

## Selected results

The following figures describe the prepared synthetic dataset and its report measures, **without additional report filters**:

| Metric | Result |
| --- | ---: |
| Unique orders in cleaned sales fact table | **239** |
| Completed orders | **48** |
| Completed orders with valid financial values | **47** |
| Completed order value (financially valid only) | **PLN 234,234.47** |
| Average valid completed order value | **PLN 4,983.71** |
| Orders flagged with data quality issues | **32** |
| Data quality audit findings | **33** |

**Metric definition:** “Completed order value” is calculated from quantity, unit price, and discount for financially valid orders with status `Completed`. It should not be interpreted as accounting-recognized revenue.

## Data preparation and quality controls

The source data deliberately contains quality problems to demonstrate realistic BI preparation. The Power Query workflow includes:

- Standardizing order IDs, order statuses, and region labels.
- Converting inconsistent price formats and parsing dates.
- Investigating missing values, duplicates, invalid quantities, and discounts.
- Identifying delivery dates earlier than order dates.
- Maintaining `HasDataQualityIssue` and `IsRevenueValid` flags.
- Separating audit findings from the cleaned analytical fact table.

**Important:** A flagged data quality issue does not necessarily make an order financially invalid. These two concepts are tracked separately.

## Data model

The main analytical model uses:

- **Fact:** `FactSalesOrders_FINAL`
- **Dimensions:** `DimCustomer`, `DimProduct`, `DimSalesperson`, `DimDate`
- **Audit:** `DataQuality_Issues` (maintained separately for exception analysis)

The date dimension supports month-level analysis, and measures are evaluated within the active report filter context.

## DAX examples

**Total orders**

```dax
Total Orders =
DISTINCTCOUNT(FactSalesOrders_FINAL[OrderID])
```

**Completed orders**

```dax
Completed Orders =
CALCULATE(
    [Total Orders],
    FactSalesOrders_FINAL[OrderStatus_Clean] = "Completed"
)
```

**Valid order value**

```dax
Valid Order Value =
SUMX(
    FILTER(
        FactSalesOrders_FINAL,
        FactSalesOrders_FINAL[IsRevenueValid] = TRUE()
    ),
    FactSalesOrders_FINAL[Quantity_Clean]
        * FactSalesOrders_FINAL[UnitPrice_Clean]
        * (1 - FactSalesOrders_FINAL[DiscountPct])
)
```

**Completed order value**

```dax
Completed Order Value =
CALCULATE(
    [Valid Order Value],
    FactSalesOrders_FINAL[OrderStatus_Clean] = "Completed"
)
```

These measures are examples of the project's use of `DISTINCTCOUNT`, `CALCULATE`, `FILTER`, and `SUMX`.

## Tools and skills demonstrated

**Power BI Desktop · Power Query (M) · DAX · Data modeling · Data validation · KPI design · Interactive filtering · Business reporting · Excel/CSV**

## Repository contents

```text
pos-manufacturing-analytics/
├── README.md
├── POS_Manufacturing_Analytics.pdf   # Exported report for viewing
├── powerbi/
│   └── POS_Manufacturing_Analytics.pbix  # Editable Power BI Desktop report
└── data/                                 # Optional: synthetic source datasets
```

The PDF and PBIX links above work when both files are committed at the specified paths. The `data/` directory is optional.

## How to view or reproduce

1. Open the **[PDF report](./POS_Manufacturing_Analytics.pdf)** to review the four report pages.
2. **[Download the PBIX file](./powerbi/POS_Manufacturing_Analytics.pbix)** and open it in **Power BI Desktop** to use the interactive report and inspect its model and measures.
3. If source CSV files are provided, update their paths in **Transform data → Data source settings** as needed, then refresh the model.

## Notes and limitations

- The dataset is simulated and intended for learning and portfolio demonstration.
- PDF export is non-interactive; some on-screen Power BI behavior cannot be reproduced in it.
- Data quality exceptions are documented rather than silently removed.
- Results are based on the project dataset and the report's validation rules, not real commercial transactions.

---

**Author:** [Krzysztof Broniszewski](https://github.com/Krzysztof-Broniszewski)  
**Project:** POS Manufacturing Analytics  
**Focus:** Business Intelligence · Data Analytics · Power BI
